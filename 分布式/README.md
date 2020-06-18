# 分布式系统

核心域：核心竞争力，核心业务 (需要投入最好的人力和资源)

支持子域： 没有，很糟糕; 有，也不足以脱颖而出(可以考虑外包)

通用子域：都有的东西, 比如认证, 发短信, 客服系统等(可以考虑购买商业解决方案或者采用开源方案)

# Spring Cloud

Spring Cloud 是规范 实现 有  Spring Cloud NetFlix and Spring Cloud Alibaba
![WX20190315-164937@2x](assets/XQxLikC.png)
![1123](assets/G2MpfMe.png)

## 注册中心  服务注册和发现

Nacos Discovery、Spring Cloud Netflix Eureka、ZooKeeper 和 Consul （原生）

## 服务消费者

rest （restTemplate）+ribbon 负载均衡 feign

## 配置中心 

Nacos Config 和 Spring Cloud Config  Apollo

## 断路器

Hystrix  Sentinel

## 网关

服务网关是微服务架构中一个不可或缺的部分。通过服务网关统一向外系统提供REST API的过程中，除了具备服务路由、均衡负载功能之外，它还具备了权限控制等功能
Zuul  Spring Cloud GateWay（原生）

