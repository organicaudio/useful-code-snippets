# Spring fundamentals

## general

There is always at least on Inversion of Control container which is called Spring **ApplicationContext**. It is possible to have multiple ApplicationContexts. In this case there is a root ApplicationContext which is used to create child ApplicationContexts.

In order to keep consistent versions of the spring framework dependencies you can import **platform-bom** as a pom into your own pom.

## configuring application context

### configuration annotation

A Configuration Annotation is used on classes which defines beans. It is an alternative to a xml config file. 

The @Bean Annotation: 

- is used on Methods
- can only be used in classes which are annotated with @Configuration
- is an alternative to @Component/ @Autowire. It allows more fine grained instantiation logic (decouples bean definition and bean declaration)

[Differences of Bean and Component](https://stackoverflow.com/questions/10604298/spring-component-versus-bean/10604537#10604537)Configuration

### bootsrapping a spring application (context)

```java
@Configuration
@ComponentScan // alternative to usage of explicit @Bean annotations. Needed for classes which are annotated with a @Component stereotype
public class SpringApp {
    private static ApplicationContext applicationContext;
 
    @Bean
    public ExampleBean exampleBean() {
        // do further declaration stuff if needed
        return new ExampleBean();
    }
 
    public static void main(String[] args) {
        this.applicationContext = 
          new AnnotationConfigApplicationContext(SpringApp.class);
 
        for (String beanName : applicationContext.getBeanDefinitionNames()) {
            System.out.println(beanName);  
        }
    }
}
```

### properties and environmental variables

The @Value annotations is used on fields, constructor parameters and method parameters. It allows to inject values from a property file or a environmental variable into a filed or a parameter. It supports the spring expressions language (SPELL).

To import a property of a property file:

```java
@PropertySource("classpath:/application.property")
@Value("${property.name}")
private String example;
```

To import a environmental property:
```java
@Value("${environmental_property_name}")
private String example;
```

### profiles

- Spring profiles allow you to load alternate configurations based on environment variables
- With @Profile() a bean can be added to a specific profile
- environmental variable to control the spring profile:  spring.profiles.active

You can set profile via:

1. Context parameter in web.xml (``<ontext-param> <param-name>spring.profiles.active</param-name><param-value>...</param-value></context-param>``)
2. WebApplicationInitializer
3. JVM System parameter (spring.profiles.active)
4. Environment variable (spring.profiles.active)
5. Maven profile (<spring.profiles.active>)
6. @ActiveProfile for unit test

You can read profile via:

1. Environment class
2. @Value(spring.profiles.active)
3. 

Examples how to activate profile from cli:

```shell
# as jvm parameter
java -jar -Dspring.profiles.active=dev app.jar

# as application arguments
java -jar app.jar --spring.profiles.active=dev

# as maven profile spring boot
mvn spring-boot:run -Dspring-boot.run.profiles=dev

# as maven profile spring 
mvn spring-boot:run -Drun.profiles=dev

```

### spring expression language SPELL

examples:

- read environmental variables: ``"${environmental_variable_name}"``
- Object creation ``"#{new Boolean(environment['spring.profiles.active'] == 'dev')"`` 

### bean scopes

To explicitly use a scope add @Scope() to Bean. Scopes:

- singleton bean (default)
- prototype bean: new instance every time it is referenced
- sessions scoped bean (web)
- request scoped bean (web)
  
### proxies

- proxies add behavior to beans like caching or transactions
- are only used if the bean is instantiated by spring

## Annotation-based configuration

### component scan

Annotation-based configuration/ component scanning is an alternative to adding beans to Application context via @Bean or xml config. 

You need to add @ComponentScan to a class. The annotation without arguments tells Spring to scan the current package and all of its sub-packages for classes which are annotated witch @Component or other stereotypes.

The **Component** annotation is a so called *generic stereotype*, which is used to mark a class which should be instantiated by the BeanFactory. The other stereotypes are **Controller**, **Service** and **Repository**, which are specializations of the @Component class. Some stereotypes bring default proxies with them.

Use **@Autowire** to inject a bean. The **@Qualifier** Annotation can be used if there are multiple implementations for a bean interface.

## autowiring

field level injection:

1. is not good because it is hard to test/ mock
2. can not control the construction  

setter level injection:

1. for optional dependecies
2. for changing dependecies (mutable variables)

constructor level injection:

1. preferred method
2. immutable

## lifecycle methods

- @PostConstruct is used on a void-method and is called after the initialization of a bean. 
- @PreDestroy is used on a void-method and is called before the bean is destroyed.

The annotations are part of java ee and therefore removed in java 11. To use them you must define them as depdency:

```xml
<dependency>
    <groupId>javax.annotation</groupId>
    <artifactId>javax.annotation-api</artifactId>
    <version>1.3.2</version>
</dependency>
```

## xml-based config (legacy)

It is *legacy*.

- xml elements are used for beans
- attributes and sub-elements are used for configuration of beans
- xml namespaces are used
- typical names are: application-config.xml, mvc-config.xml, web-application-config.xml 

## bean lifecycle

1. Initialization
2. use
3. destroy


Initialization varies for the three ways beans can be defined. This one is for xml, but it is similar to the two other ways:

1. Create ApplicationContext which wraps the BeanFactory
2. Initialize the BeanFactory
   1. Load Bean definitions (via java config, xml config, autoconfig and component scanning)
   2. BeanFactory Post-Processing (resolve SPELL or interpolation from  property files)
   3. Foreach bean: init 
      1. constructor
      2. setter (and fields)
      3. Bean Post-Processing
         1. pre init    
         2. init
         3. post init

## aspects

Aspects are:

- cross cutting concerns
- reusable blocks of code
- e.g. logging, security, transaction management, caching

Spring uses AspectJ for Aspect oriented programming (AOP), which uses byte code modification (runtime interweaving). If (vanilla) spring is used @EnableAspectJAutoProxy needs to be added to the Configuration class. An alternative for AspekctJ are JavaEE CDI interceptors (they are simpler but less flebile and apsectj is spring native).  

Nomenclature

- **Joint point** - code where advice is used
- **Pointcut** - selects a joint point
- **Advice** - code that is exectuted at join point
- **Aspect** - Module containing pointcuts and advice

@Aspect is used to mark a class to show that it contains pointcuts and advice. Pointcuts are methods marked with @Pointcut(<pointcut expression>) annotation. 

pointcut expressions: 

- @annotation - use a annotation to mark pointcut
- execution - matches method signature
- within - matches class type signature patterns
- bean - matches class name patterns
- || -  combines pointcut expressions

Advice are methods which are marked with one of the following annotations and reference the method name of a pointcut (method annotated with @Pointcut):

- Before
- After
- Around
