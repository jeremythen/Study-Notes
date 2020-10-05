# Batch

## Terms

- Tasklet

## Notes

@EnableBatchProcessing

There are 2 steps in Spring Batch:

1. Tasklet-based step
2. Chunk-based step

## Job parameters

Job instances are created using the name of the job and parameters passed by the job launcher.

If a job instance ran successfully, it is not possible to start that job instance again. A new job instance needs to be created by passing a new job parameter to the job.

Executing a job from a jar with parameters:

> java -jar linkedin-batch-02-02-end-0.0.1-SNAPSHOT.jar "item=shoes" "run.date(date)=2020/01/01"

Accessing those parameters:

```java
String item = chunkContext.getStepContext().getJobParameters().get("item").toString(); // Passed in the command line
String date = chunkContext.getStepContext().getJobParameters().get("run.date").toString();
System.out.println(String.format("The %s has been packaged on %s.", item, date));
```

## Multiple steps

```java
@Bean
public Job deliverPackageJob() {
    return this.jobBuilderFactory.get("deliverPackageJob")
            .start(packageItemStep())
            .next(driveToAddressStep())
            .next(givePackageToCustomerStep())
            .build();
}

```

## Restarting jobs

If a job is COMPLETED, it will not restart.

Only FAILED or STUCK, and these will be able to restart.

If any exception is thrown in a Spring batch, it will fail, if we don't have any other configuration to control that exception.

## Job flow

```java

.start(step1())
    .on("FAILED").to(step2()) // If fails, will only move to step2
    from(step1()) // if step1 didn't fail, then it will execute step 3
    on("*").to(step3()) // If the status is different than FAILED

```

## BatchStatuses

- ABANDONED
- COMPLETED
- FAILED
- STARTED
- STOPPED

## Exist Statuses

- COMPLETED
- EXECUTING
- FAILED
- STOPPED
- Custom Status

## Custom statuses

## Job execution decider

This is to decide what step to run based on some conditions.

1. Create a class and implement JobExecutionDecider
2. Override the FlowExecutionStatus decide method and return a result.
3. Create a bean that returns an instance of that decider
4. Then on the steps, you use .on("\*").to(decider())

## Stop transitions

```java
.end() // This will end the job and save it as COMPLETED
.stop() // This will stop the job and save the status as STOPPED
.fail() // This will end the job and save it as FAILED

```

## Listeners

- Allow logic to be interjected before or after key events
- Defined using interface implementations or annotations
- Registered at appropriate level in the configuration

### Listers interfaces available:

- JobExecutionListener
- StepExecutionListener
- ChunkListener
- SkipListener
- ItemReadListener
- ItemWriteListener
- ItemProcessListener
- RetryListener

Then you simple use before the build() method when configuring your steps.

## Reusing external flows

For this, create a bean that returns a Flow, FlowBuilder<SimpleFlow>("deliveryFlow).start(step1())...next...
And use that as a regular step in other step definition.

## Nesting jobs

In a step definition, instead of using next, use the job() method to include a job definition.

## Parallel Flows

We need to se a FlowBuilder.
Then, in your job definition, use the .split(new AsyncTaskExecutor()) method.
Then use the .add(deliveryFlow(), billingFlow()) to specify the flows to run.
This works with flows.

# Chunk-Based Step

Items read into chunks, which are processed and then written within a transaction.

- ItemReader
- ItemProcessor
- ItemWriter

The process is:

1. You specify the chunk count. The chunks are specified in the Data Store
2. The Item Reader will read the chunk from the Data Store
3. Then Item Processor will process it and when it reaches to the chunk count, it will send it to Item Writer
4. Then Item Writer will write it to the Data Store within a transaction.

## Available ItemReaders

- KafkaItemReader
- FlatFileItemReader
- HibernateCursorItemReader
- HibernatePagingItemReader
- JdbcCursorItemReader
- JdbcPagingItemReader
- JpaPagingItemReader
- MongoItemReader
- StaxEventItemReader
- JsonItemReader

Define a regular step.
Instead of using start or next, use the .<InputType, OutputType>chunck(3) method.
Then .reader(itemReader()).writer(itemWriter())
ItemReader read method will be called for each item.

### Reading flat files

Let Order be a pojo with the fields matching the column names of the flat file header.

FlatFileItemReader<Order>...
itemReader.setLinesToSkip(1) // To skip the header
itemReader.setResource(new FileSystemResource("path/to/the/file.csv"))
DefaultLineMapper<Order> lineMapper = new DefaultLineMapper<Order>();
DelimitedLineTokenizer tokenizer = new DelimitedLineTokenizer();
tokenizer.setNames(new String[] {"column1", "column2"});
lineMapper.setLineTokenizer(tokenizer);
lineMapper.setFieldSetMapper(new OrderFieldMapper());
itemReader.setLineMapper(lineMapper);
return itemReader;

Create the OrderFieldSetMapper that implements FieldSetMapper<Order>

public Order mapFieldSet(FieldSet fieldSet)...
Order order = new Order();
order.setOrderId(fieldSet.readLong("order_id));
...

### Reading databases

In the ItemReader<Order> bean:

return new JdbcCursorItemREaderBilder<Order>()
.dataSource(dataSource)
.name("jdbcCursorItemReader)
.sql("SELECT order_id, first_name FROM SHIPPED_ORDER order by order_id") // Use order by clause to specify the order of the data
.rowMapper(new OrderRowMapper())
.build();

Create the OrderRowMapper implements RowMapper<Order>...

public Order mapRow(ResultSet rs, int rowNum)...
Order order = new Order();
order.setOrderId(rs.getLong("order_id))
...

## Available ItemWriters

- KafkaItemWriter
- FlatFileItemWriter
- HibernateItemWriter
- JdbcBatchItemWriter
- JmsItemWriter
- JpaItemWriter
- MongoItemWriter
- StaxEventItemWriter
- JsonFileItemWriter

### Writing to flat files:

Create ItemWriter<Order> bean.
Create a FlatFileItemWriter<Order> itemWriter = new FlatFileItemWriter<Order>();
itemWriter.setResource(new FileSystemResource("/data/shipped_orders_output.csv"));
DelimitedLineAggregator<Order> aggregator = new DelimitedLineAggregator<Order>();
aggregator.setDelimiter(",");
BeanWrapperFieldExtractor<Order> fieldExtractor = new BeanWrapperFileExtractor<Order>();
fieldExtractor.setNames(new String[] {"column1", "column2"});
aggregator.setFieldExtractor(fieldExtractor);
itemWriter.setLineAggregator(aggregator);
return itemWriter;

### Writing to database

```java

public static String INSERT_ORDER_SQL = "insert into ... values(?, ...)"
public static String INSERT_ORDER_SQL_NAMED = "insert into ... values(:orderId, ...)"

Create a ItemWriter<Order> bean
Return a new JdbcBatchItemWriterBuilder<Order>()
    .dataSource(dataSource)
    .sql(INSERT_ORDER_SQL)
    .itemPreparedStatementSetter(new OrderItemPreparedStatementSetter())
    .build();

class OrderItemPreparedStatementSetter implements ItemPreparedStatementSetter<Order> {
    @Override
    public void setValues(Order item, PreparedStatement ps) {
        ps.setLong(1, item.getOrderId());
        ps.setString(2, item.getFirstName());
        //...
    }

}

// With named parameters:

.dataSource(dataSource)
    .sql(INSERT_ORDER_SQL)
    .beanMapped() // This is to set the name of the prop to the named parameter
    .build();


```

## ItemProcessor

This is used optionally to modify or process the data in between the read and write.

```java

@Bean
public Step chunkBasedStep() {
    return this.stepBuilderFactory.get("chunkBasedStep")
        .<Order, Order>chunk(10)
        .reader(itemReader())
        .processor(orderValidatingItemProcessor())
        .writer(itemWriter())
        .build();
}

@Bean
public ItemProcessor<Order, Order> orderValidatingItemProcessor() {
    BeanValidatingItemProcessor<Order> itemProcessor = new BeanValidatingItemProcessor<Order>();
    itemProcessor.setFilter(true);
}

// Also

public class TrackedOrderItemProcessor implements ItemProcessor<Order, TrackedOrder> {
    @Override
    public TrackedOrder process(Order item) {
        TrackedOrder trackedOrder = new TrackedOrder(item);
        trackedOrder.setTrackingNumber(UUID.randomUUID().toString());
        return trackedOrder;
    }
}

// Also chaining item processors:

.processor(compositeItemProcessor())

@Bean
public ItemProcessor<Order, TrackedOrder> compositeItemProcessor() {
    return new CompositeItemProcessorBuilder<Order, TrackedOrder>()
    .delegate(processor1(), processor2())
    .build();
}


```

## Skip logic

For not critical jobs, you can skip it and allow it not to fail.

```java

@Bean
public Step chunkBasedStep() {
    return this.stepBuilderFactory.get("chunkBasedStep")
        .<Order, Order>chunk(10)
        .reader(itemReader())
        .processor(orderValidatingItemProcessor())
        .faultTolerant()
        .skip(OrderProcessingException.class) // If this step throws this exception, it will continue working anyways
        .skipLimit(5) // It will try 5 times before finally failing
        .listener(new CustomSkipListener())
        .writer(itemWriter())
        .build();
}

class CustomSkipListener implements SkipListener<Order, TrackedOrder> {
    @Override
    public void onSkipInProcess(Order item, Throwable t) {
        System.out.println("Skipping processing of item with id: " + item.getOrderId());
    }
}

```

## Retries

```java

@Bean
public Step chunkBasedStep() {
    return this.stepBuilderFactory.get("chunkBasedStep")
        .<Order, Order>chunk(10)
        .reader(itemReader())
        .processor(orderValidatingItemProcessor())
        .faultTolerant()
        .retry(OrderProcessingException.class)
        .retryLimit(3)
        .listener(new CustomRetryListener())
        .writer(itemWriter())
        .build();
}

class CustomRetryListener implements RetryListener<Order, TrackedOrder> {

    @Override
    public <T, E extends Throwable> boolean open(RetryContext context, RetryCallback<T, E> callback) {
        if(context.getRetryCount() > 0) {
            System.out.println("Attempting retry");
        }
        return true;
    }

    @Override
    public <T, E extends Throwable> void close(RetryContext context, RetryCallback<T, E> callback) {

    }

    @Override
    public <T, E extends Throwable> void onError(RetryContext context, RetryCallback<T, E> callback) {
        if(context.getRetryCount() > 0) {
            System.out.println("Failure occurred requiring a retry");
        }
    }


}


```

## Operating jobs, scheduling, etc.

In .properties
spring.batch.job.enabled=false # This will tell Spring not to start the job on app start up.

```java
@EnableScheduling
...

@Autowired
public JobLauncher jobLauncher;

@Scheduled(cron = "0/30 * * * * *") // Cron expression. This will run every 30 seconds
public void runJob() {
    JobParametersBuilder paramBuilder = new JobParametersBuilder();
    paramBuilder.addDate("runTime", new Date());
    this.jobLauncher.run(job(), paramBuilder.toJobParameters());
}

@Bean
public Job job() {
    return this.jobBuilderFactory.get("job").start(step().build());
}


```

### Scheduler

Add the spring-boot-starter-quartz dependency.

Mke your application class extends QuartzJobBean:

```java

@SpringBootApplication
@EnableBatchProcessing
@EnableScheduling
public class BatchApplication extends QuartzJobBean {

    @Autowired
    public JobExplorer jobExplorer;

    @Autowired
    public JobLauncher jobLauncher;

    @Bean
    public Trigger trigger() {
        SimpleScheduleBuilder scheduleBuilder = SimpleScheduleBuilder
            .simpleSchedule()
            .withIntervalInSeconds(30)
            .repeatForever();
            return TriggerBuilder.newTrigger()
                .forJob(jobDetail())
                .withSchedule(scheduleBuilder)
                .build();
    }

    @Bean
    public JobDetail jobDetail() {
        return JobBuilder.newJob(BatchApplication.class)
            .storeDurably()
            .build();
    }

    @Override
    protected void executeInternal(JobExecutingContext contexts) {
        JobParameters parameters = new JobParametersBuilder(jobExplorer)
            .getNextJobParameters(job())
            .toJobParameters();

            this.jobLauncher.run(job(), parameters);
    }

    @Bean
    public Job job() {
        return this.jobBuilderFactory.get("job").incrementer(new RunIdIncrementer()).start(step()).build()
    } // An incrementer to increment the job parameters to get different job instances in every run.

}


```
