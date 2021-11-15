- [常见问题](#常见问题)
  - [Spring 和 Spring Boot 的区别是什么？](#spring-和-spring-boot-的区别是什么)
  - [讲讲 Spring IoC 框架](#讲讲-spring-ioc-框架)
  - [讲讲 Spring AOP](#讲讲-spring-aop)
- [公司](#公司)


</br></br>


# 常见问题
## Spring 和 Spring Boot 的区别是什么？
答：
- Spring 是一个 IoC 容器，用来管理 Bean，使用依赖注入实现控制反转，可以很方便的整合各种框架，提供 AOP 机制弥补 OOP 的代码重复问题，将不同类不同方法中的共同处理抽取成切面，自动注入给方法执行，比如日志记录、异常处理等。
- Spring MVC 是 Spring 对 Web 框架的一个解决方案，提供了ー个总的前端控制 Servlet，用来接收请求，然后定义了一套路由策略（URL 到 handle 的映射）及适配执行 handle，将 handle 结果使用视图解析技术生成视图，展现给前端。
- Spring Boot 是 Spring 提供的一个快速开发工具包，可以更方便、更快速地开发 Spring + Spring MVC 应用，简化了配置（约定了默认配置），整合了一系列的解决方案（starter 机制），使得 Redis、MongoDB 等可以开箱即用。

## 讲讲 Spring IoC 框架
答：
- 可以将 IoC 模式看成工厂模式的升华，IoC 就是一个大工厂，这个大工厂要生成的对象在 XML 中给出定义，然后就可以利用 Java 反射，根据 XML 中给出的类名生成相应的对象。
- 工厂模式都是在工厂方法中把对象的生成代码写死，而 Spring 容器则是由 XML 文件来定义类与类之间的关系，将工厂和对象生成两者独立开来。
- Spring IoC 就是我们把类与类之间的依赖关系在 XML 配置文件中写好，就不再自己 new 对象了，之后我们要用哪个对象就向 Spring 要，Spring 会帮我们按照我们定义的依赖关系给我们创建好相应的对象。
- `createBean()`：
  - 利用反射创建 Bean；
  - 获取 Bean 需要的属性对象，将其注入到 Bean 中。

## 讲讲 Spring AOP

![](https://upload-images.jianshu.io/upload_images/7896890-8225b1537175bd8b.png?imageMogr2/auto-orient/strip|imageView2/2/w/440/format/webp)

答：
- AOP (Aspect Of Programming)：
  - 切入点（Pointcut）：在哪些类，哪些方法上切入（where）。
  - 通知（Advice）：在方法执行的什么时间（when：方法前/方法后/方法前后）做什么（what：增强的功能）。
  - 切面（Aspect）：切面 = 切入点 + 通知，即在什么时机，什么地方，做什么增强。
  - 织入（Weaving）：把切面加入到对象，并创建出代理对象的过程。
  - 让核心业务与周边功能分离。
- 动态织入与静态织入
  - Spring AOP 采用基于运行时增强的代理技术；
    - ![](https://pic3.zhimg.com/v2-b091ac6fd64f493eaeabfeff4cee7fee_b.png)
    - JDK 代理：基于反射技术的实现；
    - CGLib 代理：基于继承的机制实现。
  - AspectJ 采用静态织入方式。
    - ![](https://pic2.zhimg.com/v2-a4f70efe3e2bb0b438ea89a3ae927011_b.png)


</br></br>


# 公司
- 2020-8 B站