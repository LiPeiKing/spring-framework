一、模块详细介绍
1、spring-aop模块
  面向切面编程时使用。Spring通过"横切"的方式将贯穿于多业务中的公共功能独立抽取出来，形成单独的切面，并指定切面的具体动作，在需要使用该功能时，动态地将该功能切入到需要的地方。

2、spring-aspects模块
  用来实现AspectJ框架的集成。而AspectJ是一个通过对java扩展出之后的框架，框架里面定义了AOP的语法，通过特殊的编译器完成编译期间的代码织入，最后生成增强之后的Class文件。

3、spring-beans模块
  完成Spring框架的基本功能，里面定义了大量和Bean有关的接口，类及注解。例如：bean定义的顶层接口BeanDefinition、bean装配相关的注解Autowired/Qualifier/Value、用来创建bean的工厂接口BeanFactory及一些具体的工厂方法等。

4、spring-context模块
  用来实现Spring上下文功能，及Spring的IOC，例如初始化Spring容器时所使用的ApplicationContext接口及常用的抽象实现类AnnotationConfigApplicatoinContext或者ClasspathXmlApplicationContext等。

5、spring-context-indexer模块
  用来创建Spring应用启动时候选组件的索引，以提高应用的启动速度。通常情况下，应用启动的时候会去扫描类路径下的所有组件，但是如果组件特别多，会导致应用启动特别缓慢。该模块可以在应用的编译器对应用的类路径下的组件创建索引，在启动的时候通过索引去加载和初始化组件，可以大大提升应用启动的速度。

6、spring-context-support模块
  用来提供Spring上下文的一些扩展模块，例如实现邮件服务、视图解析、缓存(定义了对下面几种缓存的支持：caffeine,ehcache,jcache)、定时任务调度等。

7、spring-core模块
  Spring的核心功能实现，例如：控制反转(IOC)、依赖注入(DI)、asm以及cglib的实现。

8、spring-expression模块
  提供Spring表达式语言的支持，SPEL。

9、spring-framework-bom模块
  通过该模块，可以解决Spring中的模块与其他框架整合时产生jar包版本的冲突，默认为空实现。

10、spring-instrument模块
  实现Spring对服务器的代理接口功能实现，实现的是类级别或者ClassLoader级别的代理功能。

11、spring-jcl模块
  通过适配器设计模式实现的一个用来统一管理日志的框架，对外体统统一的接口，采用"适配器类"将日志的操作全部委托给具体的日志框架，提供了对多种日志框架的支持。

12、spring-jdbc模块
  Spring对JDBC(Java Data Base Connector)功能的支持，里面定义了用于操作数据的多种API，常用的即：JdbcTemplate，通过模板设计模式将数据库的操作和具体业务分离，降低了数据库操作和业务功能的耦合。

13、spring-jms模块
  对Java消息服务的支持，对JDK中的JMS API进行了简单的封装。

14、spring-messaging模块
  实现基于消息来构建服务的功能。

15、spring-orm模块
  提供了一些整合第三方ORM框架的抽象接口，用来支持与第三方ORM框架进行整合，例如：MyBatis，Hibernate，Spring JPA等。

16、spring-oxm模块
  Spring用来对对象和xml（Object/xml）映射的支持，完成xml和object对象的相互转换。

17、spring-test模块
  Spring对Junit测试框架的简单封装，用来快速构建应用的单元测试功能及Mock测试。

18、spring-tx模块
  Spring对一些数据访问框架提供的声明式事务或者编程式事务（通过配置文件进行事务的声明）的支持。例如：Hibernate，MyBatis，JPA等。

19、spring-web模块
  用来支持Web系统的功能。例如：文件上传，与JSF的集成，过滤器Filter的支持等。

20、spring-webflux模块
  Spring5中新增的一个通过响应式编程来实现web功能的框架。内部支持了reactive和非阻塞式的功能，例如可以通过tcp的长连接来实现数据传输。webmvc的升级版，webmvc是基于servlet的，而webflux是基于reactive的。

21、spring-webmvc模块
  用来支持SpringMVC的功能，包括了和SpringMVC框架相关的所有类或者接口，例如常用的DispatcherServlet、ModelAndView、HandlerAdaptor等。另外提供了支持国际化、标签、主题、FreeMarker、Velocity、XSLT的相关类。注意：如果使用了其他类似于smart-framework的独立MVC框架，则不需要使用该模块中的任何类。

22、spring-websocket模块
    Spring对websocket的简单封装，提供了及时通信的功能，常用于一些即时通讯功能的开发，例如：聊天室。

二、模块间依赖关系
下面介绍在使用某一个模块的功能，这个模块所依赖的其他模块，后面在分析Spring源码的过程中会有大用。  
2.1、SpringCore模块   
```
spring-context:
        -spring-core
        -spring-beans
        -spring-aop
        -spring-expression
        -spring-instrument[optional]
```
2.2、SpringAOP模块
```
spring-aop:
    -spring-core
    -spring-beans
    -aspectjweaver[optional]
```
2.3、SpringJDBC模块   
```
spring-jdbc:   
    -spring-core
    -spring-beans
    -spring-tx
    -spring-context[optional]
spring-tx:
    -spring-core
    -spring-beans
    -spring-aop[optional]
    -spring-context[optional]

spring-orm:
    -spring-core
    -spring-beans
    -spring-jdbc
    -spring-tx
    -spring-aop[optional]
    -spring-context[optional]
    -spring-web[optional]

spring-oxm:
    -spring-core
    -spring-beans

spring-jms:
    -spring-core
    -spring-beans
    -spring-messaging
    -spring-tx
    -spring-aop[optional]
    -spring-context[optional]
    -spring-oxm[optional]
```


2.4、SpringWeb   
```
spring-web:
    -spring-core
    -spring-beans
    -spring-aop[optional]
    -spring-context[optional]
    -spring-oxm[optional]

spring-webmvc:   
     -spring-core
    -spring-beans
    -spring-web
    -spring-expression
    -spring-context
    -spring-aop
    -spring-context-support[optional]
    -spring-oxm[optional]

spring-websocket:
    -spring-core
    -spring-web
    -spring-context
    -spring-webmvc[optional]
    -spring-messaging[optional]

spring-messaging:
    -spring-core
    -spring-beans
    -spring-context[optional]
    -spring-oxm[optional]
```
