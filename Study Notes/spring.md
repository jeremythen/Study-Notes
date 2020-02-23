@Configuration annotation tells spring that this is a class to initiate POJOs instances, based on a method name with a @Bean annotation.
@Bean(name="thisNameOverridesMethodName")

---

Spring provides two types of IoC container implementations:
The basic one is called a bean factory.
The more advanced one is called an application context, which is compatible with the bean factory. 

---

The interfaces for the bean factory and the application context are BeanFactory and
ApplicationContext, respectively. The ApplicationContext interface is a subinterface of BeanFactory for
maintaining compatibility.

---

AnnotationConfigApplicationContext is one of the implementation of ApplicationContext.

ApplicationContext context = new AnnotationConfigApplicationContext
(SequenceGeneratorConfiguration.class); // SequenceGeneratorConfiguration has the @Configuration annotation.

---

@Component("componentName") is an annotation to let Spring know it can create POJOs from it. The string inside is it's ID. If no id is provided, the uncapitalized nonqualified class name is used.

---

Spring has 3 layers: Persistance, Service and Presentation.

---

    1. The Separation of Concerns (SoC) Principle

    Separation of concerns (SoC) is a design principle for separating a computer program into distinct sections, such that each section addresses a separate concern.

    This means that we should

    Identify the “concerns” that we need to take care of.
    Decide where we want to handle them.

---

DAO: Data Access Object, is an object in charge of accessing the database for information, from entities, etc.

DTO: Data Transfer Object, is an object in charge of keeping dat to be transfered, like a datastrucutre.

---

@Repository causes exceptions to be wrapped up as DataAccessExceptions,
which makes debugging easier

---
@ComponentScan without arguments tells Spring to scan the current package and all of its sub-packages.

@ComponentScan(basePackages = "com.example")

-

@ComponentScan(
    includeFilters = {
        @ComponentScan.Filter(
            type = FilterType.REGEX,
            pattern = {"com.apress.springrecipes.sequence.*Dao", "com.apress.springrecipes.sequence.*Service"})
    },
    excludeFilters = {
        @ComponentScan.Filter(
            type = FilterType.ANNOTATION,
            classes = {org.springframework.stereotype.Controller.class}) }
    )

---

By default, all the properties with @Autowired are required. When Spring can’t find a matching bean to
wire, it will throw an exception. If you want a certain property to be optional, set the required attribute of
@Autowired to false. Then, when Spring can’t find a matching bean, it will leave this property unset.

@Autowired(required=false)

---

Tip As of Spring Framework 4.3, if you have only a single constructor, Spring will automatically use that
constructor for autowiring. In that case, you can omit the @Autowired annotation.

---

@Primary annotation and the @Qualifier annotation.

Use @Primary over the class bean to specify that this type is the first type that Spring should override, even if there are more types.

Use @Qualifier("beanName") on the field to autowire along with the @Autowired annotation to let Spring know that for that field, it should autowire that specific bean, even if there are more types.
@Qualifier can also be applied to method parameters.

---

To initialize the Spring IoC container with multipe config classes:

AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(PrefixConfiguration.class SequenceGeneratorConfiguration.class);

Or use the @Import on another configuration classes to make present another config class:

@Configuration
@Import(PrefixConfiguration.class)
public class SequenceConfiguration {...

---

@Value("#{datePrefixGenerator}") is used to set a default value to a field, setter method, method parameter, etc.
private PrefixGenerator prefixGenerator;

---

Spring Expression Language (SpEL)

---

@Resource and @Inject are Java annotations and try to do the same as Spring's @Autowired annotation.

With @Inject, a customize annotation needs to be created to specify what to inject if autowiring by name:
@Inject @DataPrefixAnnotation
private PrefixGenerator prefixGenerator;
...

---

 Singleton is the default scope of all beans.

 @Scope("prototype") to create a new bean each time getBean() is called.

 ---

@PropertySource("classpath:discounts.properties") specifies a key value property file to be used in a class.
@Value("${namefromprops:defaultValue}" extracts the value of namefromprops in the property file.

---

To inject a file in the classpath to a Spring Resource object:

@Value("classpath:banner.txt")
private Resource banner;

---

To load manually from different sources:

Resource resource = new ClassPathResource("discounts.properties");
//Resource resource = new ClassPathResource("discounts.properties");
//Resource resource = new UrlResource("http://www.apress.com/")
Properties props = PropertiesLoaderUtils.loadProperties(resource);
Properties props = PropertiesLoaderUtils.loadProperties(resource);

---


@Bean(initMethod = "openFile", destroyMethod = "closeFile")

---

AOP

@After("execution(* *.*(..))")
@Before("execution(* *.*(..))")
@AfterReturning("execution(* *.*(..))")
@AfterThrowing("execution(* *.*(..))")

@AfterReturning(pointcut = "execution(* *.*(..))", returning = "result")
public void logAfterReturning(JoinPoint joinPoint, Object result) {

@AfterThrowing(pointcut = "execution(* *.*(..))", throwing = "e")
public void logAfterThrowing(JoinPoint joinPoint, Throwable e) {

When using @Around, remember to call the proceed() method on the proceedingJoinPoint object and return the Object returned by that method.

The @Order(1) annotation goes on the class, not on methods.

To reuse a pointcut definition:
@Pointcut("execution(* *.*(..))")
private void reusedPointcut() {} // Empty because it will not execute, it's just a definition.

@Pointcut("annotation(com.myapp.CustomAnnotation)")
public void loggingOperation() {}

@Pointcut(within(com.myapp.package1.*)) // matches all join points within this package.
@Pointcut(within(com.myapp.package1..*)) // with 2 dots, matches all join points within this package and it´s subpackages.

within(ArithmeticCalculator+) || within(UnitCalculator+) // Mathes classes that implement either of these interfaces.

@Before("execution(* Persona.setName(String)) && target(target) && args(name)")
public void withArgs(Object target, String name) {

//Introductions, to simulate multiple inheritance.
@DeclareParents(value = "com.myapp.ArithmeticCalculatorImpl", defaultImpl = MaxCalculatorImpl.class)
public MaxCalculator maxCalculator;

---

Concurrency:

Spring’s TaskExecutor

private SimpleAsyncTaskExecutor asyncTaskExecutor;
@Autowired

... SyncTaskExecutor ...
... TaskExecutorAdapter ...
... ThreadPoolTaskExecutor ...

syncTaskExecutor.execute(task);
taskExecutorAdapter.submit(task);
asyncTaskExecutor.submit(task);

for (int i = 0; i < 500; i++)
    threadPoolTaskExecutor.submit(task);

---

Application Events:


CheckoutEvent extends ApplicationEvent
ApplicationEventPublisherAware
implements ApplicationListener<CheckoutEvent> 
@EventListener

---


Views are usually JSP templates written with the Java Standard
Tag Library (JSTL).


A Spring MVC controller—often referred to as a dispatcher servlet—
implements one of Sun’s core Java EE design patterns called Front Controller. It acts as the front controller
of the Spring MVC framework, and every web request must go through it so that it can manage the entire
request-handling process.


HandlerInterceptor to intercept request before and after.








