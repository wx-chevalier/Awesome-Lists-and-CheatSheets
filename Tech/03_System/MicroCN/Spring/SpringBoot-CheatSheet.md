# Spring Boot CheatSheet

Spring Boot 应用本质上就是一个基于 Spring 框架的应用，它是 Spring 对“约定优先于配置”理念的最佳实践产物，它能够帮助开发者更快速高效地构建基于 Spring 生态圈的应用；最重要的 4 大核心特性包括了自动配置、起步依赖、Actuator、命令行界面(CLI)。

可以在 [Spring Initializr](https://start.spring.io/) 动态地选择需要的组件，对于 Spring 框架/生态的讨论，以及 IOC/DI 等机制原理的分析参考 [Spring CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets/blob/master/Backend/WebFramework/Java/Spring-CheatSheet.md)

```java
// @SpringBootApplication 整合了 @Configuration + @ComponentScan + @EnableAutoConfiguration，其会自动进行组件扫描与配置
@SpringBootApplication
public class FooApplication {

  public static void main(String[] args) {
    // Bootstrap the application
    SpringApplication.run(FooApplication.class, args);
  }
}
```

- @Configuration: Marks a class as a config class using Spring's Java based configuration
- @ComponentScan: Enables component-scanning so that web controller classes can be automatically registered as beans in the Spring application context
- @EnableAutoConfiguration: Configures the application based on the dependencies

# 依赖声明与注入

## 依赖声明

### 注解声明

```java
@Component
public class MyComponent {}
```

在 Spring2.0 之前的版本中，@Repository 注解可以标记在任何的类上，用来表明该类是用来执行与数据库相关的操作（即 dao 对象），并支持自动处理数据库操作产生的异常

在 Spring2.5 版本中，引入了更多的 Spring 类注解：@Component,@Service,@Controller。@Component 是一个通用的 Spring 容器管理的单例 bean 组件。而@Repository, @Service, @Controller 就是针对不同的使用场景所采取的特定功能化的注解组件。

因此，当你的一个类被@Component 所注解，那么就意味着同样可以用@Repository, @Service, @Controller 来替代它，同时这些注解会具备有更多的功能，而且功能各异。

最后，如果你不知道要在项目的业务层采用@Service 还是@Component 注解。那么，@Service 是一个更好的选择。

```java
@Configuration
public class TestConfig {
    @Bean(name="helloClient")
    public HessianProxyFactoryBean helloClient() {
        HessianProxyFactoryBean factory = new HessianProxyFactoryBean();
        ...
        return factory;
    }
}
```

### Conditional Configuration | 条件化配置

Class conditions allow us to specify that a configuration bean will be included if a specified class is present.

```java
@Configuration
@ConditionalOnClass(DataSource.class)
public class MySQLAutoconfiguration {
  //...
}
```

也可以根据某个 Bean 是否存在来决定是否需要创建 Bean:

```java
@Bean
@ConditionalOnBean(name = "dataSource")
@ConditionalOnMissingBean
public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
    LocalContainerEntityManagerFactoryBean em
      = new LocalContainerEntityManagerFactoryBean();
    ...
    return em;
}
```

还可以根据是否存在某个属性配置来决定是否需要创建某个 Bean:

```java
@Bean
@ConditionalOnProperty(
  name = "usemysql",
  havingValue = "local")
@ConditionalOnMissingBean
public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();
    ...
    return dataSource;
}
```

```java
// Defining Condition that checks if the JdbcTemplate is available on the classpath
//
// Conditions are used by the auto-configuration mechanism of Spring Boot
// There are several configuration classes in the spring-boot-autoconfigure.jar
// which contribute to the configuration if specific conditions are met
public class JdbcTemplateCondition implements Condition {
  @Override
  public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
    try {
      context.getClassLoader().loadClass("org.springframework.jdbc.core.JdbcTemplate");
      return true;
    } catch (Exception e) {
      return false;
    }
  }
}

// Use a custom condition class to decide whether a Bean should be created or not
@Conditional(JdbcTemplateCondition.class)
public class MyService {
  ...
}
```

| 条件化注解                      | 配置生效条件                                            |
| ------------------------------- | ------------------------------------------------------- |
| @ConditionalOnBean              | 配置了某个特定 bean                                     |
| @ConditionalOnMissingBean       | 没有配置特定的 bean                                     |
| @ConditionalOnClass             | Classpath 里有指定的类                                  |
| @ConditionalOnMissingClass      | Classpath 里没有指定的类                                |
| @ConditionalOnExpression        | 给定的 Spring Expression Language 表达式计算结果为 true |
| @ConditionalOnJava              | Java 的版本匹配特定指或者一个范围值                     |
| @ConditionalOnProperty          | 指定的配置属性要有一个明确的值                          |
| @ConditionalOnResource          | Classpath 里有指定的资源                                |
| @ConditionalOnWebApplication    | 这是一个 Web 应用程序                                   |
| @ConditionalOnNotWebApplication | 这不是一个 Web 应用程序                                 |

## 作用域与生命周期

Spring 中为 Bean 定义了 5 种作用域，分别为 Singleton(单例), Prototype(原型), Request,Session 和 Global Session:

- Singleton, 单例模式，Spring IoC 容器中只会存在一个共享的 Bean 实例，无论有多少个 Bean 引用它，始终指向同一对象。Singleton 作用域是 Spring 中的缺省作用域，也可以显式的将 Bean 定义为 Singleton 模式

- Prototype, 原型模式，每次通过 Spring 容器获取 prototype 定义的 bean 时，容器都将创建一个新的 Bean 实例，每个 Bean 实例都有自己的属性和状态，而 Singleton 全局只有一个对象。根据经验，对有状态的 bean 使用 prototype 作用域，而对无状态的 bean 使用 Singleton 作用域。

- Request, 在一次 Http 请求中，容器会返回该 Bean 的同一实例。而对不同的 Http 请求则会产生新的 Bean，而且该 bean 仅在当前 Http Request 内有效。

- Session, 在一次 Http Session 中，容器会返回该 Bean 的同一实例。而对不同的 Session 请求则会创建新的实例，该 bean 实例仅在当前 Session 内有效。

- Global Session, 在一个全局的 Http Session 中，容器会返回该 Bean 的同一个实例，仅在使用 portlet context 时有效。

可以通过 @Scope 注解来指定作用域。Spring 容器可以管理 Singleton 作用域下 Bean 的生命周期，在此作用域下，Spring 能够精确地知道 Bean 何时被创建，何时初始化完成，以及何时被销毁。而对于 prototype 作用域的 Bean，Spring 只负责创建，当容器创建了 Bean 的实例后，Bean 的实例就交给了客户端的代码管理，Spring 容器将不再跟踪其生命周期，并且不会管理那些被配置成 prototype 作用域的 Bean 的生命周期。Spring 中 Bean 的生命周期的执行是一个很复杂的过程，读者可以利用 Spring 提供的方法来定制 Bean 的创建过程。Spring 容器在保证一个 Bean 实例能够使用之前会做很多工作：

![image](https://user-images.githubusercontent.com/5803001/47768779-677b0500-dd14-11e8-9f33-f06dbbebd08b.png)

我们常用的生命周期的 Hook 方法就是在其创建后与销毁之前：

```java
@PostConstruct
public void initAfterStartup() {
    ...
}

@PreDestroy
public void cleanupBeforeExit() {
    ...
}
```

对于使用 Bean 注解的对象，可以添加 destroyMethod 等参数来介入其生命周期：

```java
@Bean(destroyMethod = "close")
public MyBean myBean(){...
```

### Application LifeCycle | 应用生命周期

Spring Boot 为我们提供了两个接口，CommandLineRunner 与 ApplicationRunner，它们能够在应用启动之后执行部分业务逻辑。CommandLineRunner 能够允许我们访问到应用的启动参数：

```java
@Component
public class CommandLineAppStartupRunner implements CommandLineRunner {
  private static final Logger logger = LoggerFactory.getLogger(
    CommandLineAppStartupRunner.class
  );

  @Override
  public void run(String... args) throws Exception {
    logger.info(
      "Application started with command-line arguments: {} . \n To kill this application, press Ctrl + C.",
      Arrays.toString(args)
    );
  }
}
```

ApplicationRunner 则是对启动参数进行了二次封装：

```java
@Component
public class AppStartupRunner implements ApplicationRunner {
  private static final Logger logger = LoggerFactory.getLogger(
    AppStartupRunner.class
  );

  @Override
  public void run(ApplicationArguments args) throws Exception {
    logger.info(
      "Your application started with option names : {}",
      args.getOptionNames()
    );
  }
}
```

## 配置管理

Spring Boot 的一大特性即是外置所有的配置，并且提供了多种配置访问方式；首先我们可以通过动态地指定配置文件的方式来完成不同环境下的配置文件加载：

```sh
# 在本地跑时，默认是 local，在其它环境跑时，要通过 -Dspring.profiles.active= 来指定
spring.profiles.active=local
```

当某些属性的值需要配置的时候，我们一般会在 application.properties 文件中新建配置项，然后在 bean 中使用 @Value 注解来获取配置的值：

```java
// jdbc.mysql.url=jdbc:mysql://localhost:3306/sampledb

// 配置数据源
@Configuration
public class HikariDataSourceConfiguration {

    @Value("jdbc.mysql.url")
    public String url;
    ...
    @Bean
    public HikariDataSource dataSource() {
        HikariConfig hikariConfig = new HikariConfig();
        hikariConfig.setJdbcUrl(url);
        ...
        return new HikariDataSource(hikariConfig);
    }
}
```

对于更为复杂的配置，Spring Boot 提供了更优雅的实现方式，那就是 @ConfigurationProperties 注解：

```java
@Configuration
@PropertySource("classpath:configprops.properties")
@ConfigurationProperties(prefix = "mail")
public class ConfigProperties {

    public static class Credentials {
        private String authMethod;
        private String username;
        private String password;

       // standard getters and setters
    }
    private String host;
    private int port;
    private String from;
    private Credentials credentials;
    private List<String> defaultRecipients;
    private Map<String, String> additionalHeaders;

    // standard getters and setters
}

// 使用的时候直接注入
@AutoWired
public ConfigProperties config;
```

```sh
#Simple properties
mail.host=mailer@mail.com
mail.port=9000
mail.from=mailer@mail.com

#List properties
mail.defaultRecipients[0]=admin@mail.com
mail.defaultRecipients[1]=owner@mail.com

#Map Properties
mail.additionalHeaders.redelivery=true
mail.additionalHeaders.secure=true

#Object properties
mail.credentials.username=john
mail.credentials.password=password
mail.credentials.authMethod=SHA1
```

也可以为配置类添加校验：

```java
@Length(max = 4, min = 1)
private String authMethod;
```

## 端口设置

# Controller | 请求处理

传统的 Spring MVC 基于 Servlet API 构建，使用单请求单线程处理的同步阻塞型模型；而 Spring WebFlux 则是 Reactive Stack，能够充分利用现代多核处理器的特性，从底层机制上保证了对于海量并发请求处理的能力。WebFlux 使用 Netty, Servlet 3.1+ Containers 替代传统的 Servlet Containers，使用 Reactive Stream Adapters 替代 Servlet API，使用 Spring Security Reactive 替代 Spring Security，使用 Spring Data Reactive Repositories 替代 Spring Data Repositories。

![](https://docs.spring.io/spring/docs/current/spring-framework-reference/images/spring-mvc-and-webflux-venn.png)

## 路由与参数

```java
@RestController
@RequestMapping("/persons")
class PersonController {

  @GetMapping("/{id}")
  public Person getPerson(@PathVariable Long id) {
    // ...
  }

  @PostMapping
  @ResponseStatus(HttpStatus.CREATED)
  public void add(@RequestBody Person person) {
    // ...
  }
}
```

## 请求校验

Spring 为我们提供了开箱即用的简单校验，当定义某个 REST 端点之后，可以针对 PathVariable 与 RequestParameter 设置某个值是否为必须：

```java
@GetMapping("/hello/{name}")
private String hello(@PathVariable(value = "name", required = true) String name){
    //...
}

@GetMapping("/name")
private ResponseEntity<?> queryPerson(@RequestParam(value = "query", required = false) String query) {
    // ...
}
```

对于复杂请求体的验证，可以使用 Spring 内置的 [JSR 303 Bean Validation](http://beanvalidation.org/1.0/spec/) 提供的 NotNull, Max, Min 等等注解：

```java
public class Message {
  @NotNull
  private String title;

  @NotNull
  private String message;
// getters/setters/etc
}
```

然后在 Controller 中注解响应体：

```java
@PostMapping
public ResponseEntity<?> createMessage(@Valid @RequestBody Message message) {
    // ...
}
```

如果我们需要去自定义校验器，则可以选择去扩展 ConstraintValidator 接口：

```java
public class InRangeValidator implements ConstraintValidator<InRange, Integer> {
  private int min;
  private int max;

  @Override
  public void initialize(InRange constraintAnnotation) {
    this.min = constraintAnnotation.min();
    this.max = constraintAnnotation.max();
  }

  @Override
  public boolean isValid(Integer value, ConstraintValidatorContext context) {
    return value == null || (value >= min && value <= max);
  }
}

// 扩展 InRange 接口，添加自定义属性
@Target({ ElementType.METHOD, ElementType.FIELD, ElementType.PARAMETER })
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Constraint(validatedBy = { InRangeValidator.class })
public @interface InRange {
  String message() default "Value is out of range";

  Class<?>[] groups() default {  };

  Class<? extends Payload>[] payload() default {  };

  int min() default Integer.MIN_VALUE;

  int max() default Integer.MAX_VALUE;
}
```

在使用的时候，直接注解即可：

```java
@NotNull(groups = {Existing.class, New.class})
@InRange(
    min=18,
    message = "User must be at least 18 years old",
    groups = {Existing.class, New.class}
)
private Integer age;
```

最后，我们还可以自定义返回的错误格式，譬如以 JSON 的方式返回：

```java
@ExceptionHandler
@ResponseStatus(HttpStatus.BAD_REQUEST)
public ErrorResponse handleException(MethodArgumentNotValidException exception) {

    String errorMsg = exception.getBindingResult().getFieldErrors().stream()
            .map(DefaultMessageSourceResolvable::getDefaultMessage)
            .findFirst()
            .orElse(exception.getMessage());

    return ErrorResponse.builder().message(errorMsg).build();
}
```

## 响应

# Service | 服务

## Logging | 日志

## 日志配置

对外接口统一拦截捕获，避免异常向外系统传播，自身系统无法感知问题。

严格规范日志输出等级，尤其 Error 级别。影响业务进行或意料外异常输出 Error 级别，Error 级别日志统一输出到独立文件，并接入 xflush 系统错误监控告警。做到 Error 日志输出即为需要人为介入处理。为了避免干扰，对现有 Error 做降噪检查。

服务层日志统一输出，包括耗时、接口成功标识、业务成功标识，为监控做准备。

所有日志 traceId 的统一输出。通过扩展 ch.qos.logback.classic.pattern.ClassicConverter，现实 traceId 自动输出。这极大的提升了系统运维效率。

```xml
<appender name="ERROR-APPENDER"
          class="ch.qos.logback.core.rolling.RollingFileAppender">
    <file>${LOG_PATH}/common-error.log</file>
    <!-- Error 级别过滤 -->
    <filter class="ch.qos.logback.classic.filter.LevelFilter">
      <level>ERROR</level>
      <onMatch>ACCEPT</onMatch>
      <onMismatch>DENY</onMismatch>
  </filter>
    <encoder>
        <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ${LOG_LEVEL_PATTERN:-%5p} - [%thread] : %m%n${LOG_EXCEPTION_CONVERSION_WORD:-%wEx}
        </pattern>
    </encoder>
    <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
        <!-- 按天滚动，可根据实际量调整单位 -->
        <fileNamePattern>${LOG_PATH}/common-error.log.%d{yyyy-MM-dd}
        </fileNamePattern>
        <maxHistory>15</maxHistory>
    </rollingPolicy>
</appender>
```

```xml
<root level="INFO">
    <!-- root中增加Error输出配置 -->
    <appender-ref ref="ERROR-APPENDER" />
</root>

<logger name="testLog" level="INFO"
        additivity="false">
    <appender-ref ref="WORK_SHIFT_CORE_MONITOR_LOG" />
    <!-- 每个logger增加ERROR输出 -->
    <appender-ref ref="ERROR-APPENDER" />
</logger>
```

## 缓存

Spring Cache 为我们提供了非常便捷的方法调用缓存功能，在依赖中引入 spring-boot-starter-cache:

```groovy
dependencies {
    compile("org.springframework.boot:spring-boot-starter-cache")
}
```

然后在 Application 类中添加 `@EnableCaching` 注解，这样我们在进行方法调用时可以缓存调用结果：

```java
@Cacheable("books")
public Book getByIsbn(String isbn) {
    ...
}
```

# Storage | 数据访问

## Spring JDBC Template

## MyBatis

## Redis

# Test | 测试

## 请求

```java
// Testing classes in Spring Boot
@RunWith(SpringJUnit4ClassRunner.class)
// Load context via Spring Boot
@SpringApplicationConfiguration(classes = ReadinglistApplication.class)
@WebAppConfiguration
public class ReadinglistApplicationTests {

  // Test that the context successfully loads (the method can be empty -> the test will fail if the context cannot be loaded)
  @Test
  public void contextLoads() {}
}
```

## 服务

```java
// Integration test by loading Springs application context
// To to integration testing with Spring, all components of the application have to be configured and wired up.
// Instead of doing this by hand we can use Spring's SpringJUnit4ClassRunner.
// It helps load a Spring application context in JUnit-based application tests.
// This method with the @ContextConfiguration annotation doesn't apply extenal properites (application.properties) and logging
// @ContextConfiguration specifies how to load the application context: A configuraiton class is passed to it as a parameter
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = PlaylistConfiguration.class)
public class PlaylistServiceTests {
  @Autowired
  private PlaylistService playlistService;

  @Test
  public void testService() {
    Playlist playlist = playlistService.findByName("X-Mas Songs");
    assertEquals("X-Mas Songs", playlist.getName());
    assertEquals(12, playlist.countSongs());
  }
}
```

## 数据存储

```java
@SpringBootTest
@Transactional
class MySpec extends Specification {

  @Autowired
  MyRepository myRepo

  def "Persist an entity"() {
    given:
    MyEntity entity = new MyEntity()

    when:
    myRepo.saveAndFlush(entity)

    then:
    myRepo.count() == 1
  }

  def "Persist another entity"() {
    given:
    MyEntity entity = new MyEntity()

    when:
    myRepo.saveAndFlush(entity)

    then:
    myRepo.count() == 1
  }
}
```

# Links

- https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html#webflux-ann-modelattrib-methods
- https://www.baeldung.com/spring-jdbc-jdbctemplate
