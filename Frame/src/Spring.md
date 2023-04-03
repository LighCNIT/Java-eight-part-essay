### 什么是IOC？
- IOC就是控制反转。它是一种思想不是一个技术实现。描述的是：Java开发领域对象的创建及管理问题
### IOC解决了什么问题？
- IoC 的思想就是两方之间不互相依赖，由第三方容器来管理相关资源。这样有什么好处呢？
   - 对象之间的耦合度或者说依赖程度降低；
   - 资源变的容易管理；比如你用 Spring 容器提供的话很容易就可以实现一个单例。
### 什么是AOP？
- AOP：Aspect oriented programming 面向切面编程，AOP 是 OOP（面向对象编程）的一种延续。
### AOP解决了什么问题？
- 通过上面的分析可以发现，AOP 主要用来解决：
  - 在不改变原有业务逻辑的情况下，增强横切逻辑代码，
  - 根本上解耦合，避免横切逻辑代码重复。
### @Autowired和@Resource的区别
- @Autowired是spring提供的注解，@Resource是jdk提供的注解
- @Autowired默认注入方式是byType（根据类型匹配），@Resource默认注入方式是byName（根据名称匹配）
- 当一个接口有多个实现类的情况下，@Autowired和@Resource都需要名称才能正确匹配到对应的Bean。Autowired可以通过@Qualifier注解显式指定名称，@Resource可以通过name属性指定名称
### @Transactional注解哪些情况下会失效？
- 非public方法修饰
- @Transactional 注解属性 propagation 设置错误
- @Transactional 注解属性 rollbackFor 设置错误（默认unchecked）
- 同一个类中方法调用，因为没有生成代理对象
- 异常被你的 catch“吃了”导致@Transactional失效
- 数据库引擎不支持事务
### spring框架中用到了哪些设计模式？
- 工厂设计模式：Spring使用工厂模式通过BeanFactory，ApplicationContext创建bean对象
- 代理设计模式：Spring AOP功能的实现
- 单例设计模式：Spring中的Bean默认是单例的
- 模版方法模式：Spring中jdbcTemplate、hibernateTemplate等以template结尾的对数据库操作的类，它们就使用到了模版方法模式
- 包装器设计模式：我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- 观察者设计模式：Spring事件驱动模型就是观察者模式的经典运用
- 适配器模式：Spring AOP的增强或通知（Advice）使用到了适配器模式、Spring MVC中也用到了适配器模式适配Controller