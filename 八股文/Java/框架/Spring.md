- [常见问题](#常见问题)
  - [Spring 和 Spring Boot 的区别是什么？](#spring-和-spring-boot-的区别是什么)
- [公司](#公司)


</br></br>


# 常见问题
## Spring 和 Spring Boot 的区别是什么？
答：
- Spring 是一个 IoC 容器，用来管理 Bean，使用依赖注入实现控制反转，可以很方便的整合各种框架，提供 AOP 机制弥补 OOP 的代码重复问题，将不同类不同方法中的共同处理抽取成切面，自动注入给方法执行，比如日志记录、异常处理等。
- Spring MVC 是 Spring 对 Web 框架的一个解决方案，提供了ー个总的前端控制 Servlet，用来接收请求，然后定义了一套路由策略（URL 到 handle 的映射）及适配执行 handle，将 handle 结果使用视图解析技术生成视图，展现给前端。
- Spring Boot 是 Spring 提供的一个快速开发工具包，可以更方便、更快速地开发 Spring + Spring MVC 应用，简化了配置（约定了默认配置），整合了一系列的解决方案（starter 机制），使得 Redis、MongoDB 等可以开箱即用。


</br></br>


# 公司
- 2020-8 B站