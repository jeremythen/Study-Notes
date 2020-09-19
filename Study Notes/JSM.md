# JMS Specification and MOM

- Set of interfaces and terms implemented by a provider
- Message-oriented middleware (MOM)
- JMS providers furnish implementations in APIs
- A few types of MOMs (ActiveMQ, RabbitMQ, JBossMQ, etc.)

# Two Messaging Domain Types

- Point to point (PTP)
  - MSG is published to queue by a producer
  - MSG is read and removed by a consumer
  - Good for one consumer
- Publish/subscribe (pub/sub)
  - Operates around Topics
    - MSG is published to a topic by a producer
    - MSG is read by one or more subscribers
    -

# JmsTemplate

```java
@EnableJms
@SpringBootApplication
public class App {

    public static void main(String... args) {
        // ...

        SpringApplication.run(App.class, args);
        ConfigurableApplicationContext context = SpringApplication.run(App.class, args);

        Sender sender = context.getBean(Sender.class);

        // order-queue is the message queue or destination. The second is the data.
        sender.sendMessage("order-queue", "Hello!");

    }

    @Bean
    public JmsListenerContainerFactory warehouseFactory(ConnectionFactory factory, DefaultJmsListenerContainerFactoryConfigurer configurer) {
        DefaultJmsListenerContainerFactory containerFactory = new defaultJmsListenerContainerFactory();
        configurer.configure(containerFactory, factory);
        return containerFactory;
    }

}

@Component
public class Receiver {

    // Listening from order-queue. containerFactory specifies the MOM, which we named warehouseFactory.
    @JmsListener(destination = "order-queue", containerFactory="warehouseFactory")
    public void receiveMessage(String message) {
        System.out.println("Order received: " +  message);
    }

    @Bean
    public ActiveMQConnectionFactory connectionFactory() {
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory("user", "pass", "tcp://localhost:61616");
        return factory;
    }

    @Bean
    public JmsTemplate jmsTemplate() {
        return new JmsTemplate(connectionFactory());
    }

}

@Component
public class Sender {

    @Autowired
    private JmsTemplate jmsTemplate;

    public void sendMessage(String destination, String message) {
        jmsTemplate.convertAndSend(destination, message);
    }


}


```

# What is a Message Queue?

- A collection of JMS messages on a MOM or MQ server (can contain queues and topics)
- Retain messages until a consumer retrieves them
- Retrieved messages are pulled in the order they are received first-in-first-out (FIFO)

# JMS Spec Provides Five Basic Message Types

- Streams StreamMessages
- Maps MapMessages
- Text - TextMessages
  - JSON or XML
- Object - ObjectMessages
- Bytes - BytesMessages
  - Images, sound, music files
