### 什么是SpringBoot自动装配？
- 所谓自动装配就是通过注解或者一些简单的配置就能在SpringBoot的帮助下实现某功能
- 实际上 Spring Framework 早就实现了这个功能。Spring Boot 只是在其基础上，通过 SPI 的方式，做了进一步优化。
> SpringBoot 定义了一套接口规范，这套规范规定：SpringBoot 在启动时会扫描外部引用 jar 包中的META-INF/spring.factories文件，将文件中配置的类型信息加载到 Spring 容器（此处涉及到 JVM 类加载机制与 Spring 的容器知识），并执行类中定义的各种操作。对于外部 jar 来说，只需要按照 SpringBoot 定义的标准，就能将自己的功能装置进 SpringBoot。
### SpringBoot是如何实现自动装配的？
*在于下面三个核心注解*

- @EnableAutoConfiguration：启用springboot的自动配置机制
> EnableAutoConfiguration 只是一个简单地注解，自动装配核心功能的实现实际是通过 AutoConfigurationImportSelector类。它可以通过关键方法selectImports（）
*获取所有符合条件的类的全限定类名，最终通过SpringFactories.loadSpringFactories从META-INF/spring.factories加载自动配置类到IOC容器里*
当然并不一定所有的配置类都会加载，它会根据@ConditionalOnXXX注解筛选。
- @Configuration：允许在上下文注册额外的bean或者导入其他配置类
- @ComponentScan： 扫描被@Component (@Service,@Controller)注解的 bean，注解默认会扫描启动类所在的包下所有的类 ，可以自定义不扫描某些 bean。如下图所示，容器中将排除TypeExcludeFilter和AutoConfigurationExcludeFilter。
> 总结来说Spring Boot 通过@EnableAutoConfiguration开启自动装配，通过 SpringFactoriesLoader 最终加载META-INF/spring.factories中的自动配置类实现自动装配，自动配置类其实就是通过@Conditional按需加载的配置类，想要其生效必须引入spring-boot-starter-xxx包实现起步依赖
### 如何实现一个starter？
- 创建工程
- 引入SpringBoot相关依赖
- 创建自己的XXAutoConfiguration并使用@bean加载相关bean
- 最后在工程的resource目录下创建META-INF/spring.factories写上XXAutoConfiguration类全限定名



