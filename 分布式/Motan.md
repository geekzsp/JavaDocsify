# Motan

## What

Motan是一套高性能、易于使用的分布式远程服务调用(RPC)框架。

Motan是一套基于java开发的RPC框架，除了常规的点对点调用外，Motan还提供服务治理功能，包括服务节点的自动发现、摘除、高可用和负载均衡等。Motan具有良好的扩展性，主要模块都提供了多种不同的实现，例如支持多种注册中心，支持多种rpc协议等。

## Why   为什么要使用，解决了什么问题。有什么优点。和竞品对比

* 支持通过spring配置方式集成，无需额外编写代码即可为服务提供分布式调用能力。
* 支持集成consul、zookeeper等配置服务组件，提供集群环境的服务发现及治理能力。
* 支持动态自定义负载均衡、跨机房流量调整等高级服务调度能力。
* 基于高并发、高负载场景进行优化，保障生产环境下RPC服务高可用。

!>  与Dubbo 对比。为什么要使用Motan 

当时选择Motan 是因为那个时候Dubbo已经停止维护很长时间了。最近一次更新也是在2014年。 (不过 在2017年底 Dubbo重启维护了) 加上Motan是微博开源了。也是经过了大规模生产实践的考验
所以就选择了Motan。 

## How  怎么实现的。 原理。  怎么用 

### 架构概述

Motan中分为服务提供方(RPC Server)，服务调用方(RPC Client)和服务注册中心(Registry)三个角色。

* Server提供服务，向Registry注册自身服务，并向注册中心定期发送心跳汇报状态；
* Client使用服务，需要向注册中心订阅RPC服务，Client根据Registry返回的服务列表，与具体的Sever建立连接，并进行RPC调用。
* 当Server发生变更时，Registry会同步变更，Client感知后会对本地的服务列表作相应调整。

三者的交互关系如下图：

![](assets/14612349319195.jpg)

### 代码模块

Motan框架中主要有register、transport、serialize、protocol几个功能模块，各个功能模块都支持通过**SPI**进行扩展，各模块的交互如下图所示：

![](assets/14612352579675.jpg)

**register**

支持`Consul`或者`Zookeeper`作为注册中心 
用来和注册中心进行交互，包括注册服务、订阅服务、服务变更通知、服务心跳发送等功能；Server端会在系统初始化时通过register模块注册服务，Client端在系统初始化时会通过register模块订阅到具体提供服务的Server列表，当Server 列表发生变更时也由register模块通知Client。

**protocol**

用来进行RPC服务的描述和RPC服务的配置管理，这一层还可以添加不同功能的filter用来完成统计、并发限制等功能。

**serialize**

将RPC请求中的参数、结果等对象进行序列化与反序列化，即进行对象与字节流的互相转换；默认使用对java更友好的hessian2进行序列化。

**transport**

用来进行远程通信，默认使用**Netty nio**的TCP长链接方式。

**cluster**

Client端使用的模块，cluster是一组可用的Server在**逻辑上的封装**，包含若干可以提供RPC服务的Server，实际请求时会根据不同的高可用与负载均衡策略选择一个可用的Server发起远程调用。

在进行RPC请求时，Client通过代理机制调用cluster模块，cluster根据配置的HA和LoadBalance选出一个可用的Server，通过serialize模块把RPC请求转换为字节流，然后通过transport模块发送到Server端。

![](assets/14612385789967.jpg)

Client端订阅Service后，会从Registry中得到能够提供对应Service的一组Server，Client把这一组Server看作一个提供服务的cluster。当cluster中的Server发生变更时，Client端的register模块会通知Client进行更新。

### 处理调用异常

* 业务代码异常
  当调用的远程服务出现异常时，Motan会把Server业务中的异常对象抛出到Client代码中，与本地调用逻辑一致。

>注意:如果业务代码中抛出的异常类型为Error而非Exception（如OutOfMemoryError），Motan框架不会直接抛出Error，而是抛出包装了Error的MotanServiceException异常。

* MotanServiceException
  使用Motan框架将一个本地调用改为RPC调用后，如果出现网络问题或服务端集群异常等情况，Motan会在Client调用远程服务时抛出MotanServiceException异常，业务方需要自行决定后续处理逻辑。

* MotanFrameworkException
  框架异常，比如系统启动、关闭、服务暴露、服务注册等非请求情况下出现问题，Motan会抛出此类异常。

### 负载均衡

* ActiveWeight(缺省)  低并发度优先： referer 的某时刻的 call 数越小优先级越高
* Random
* RoundRobin 轮询
* Consistent 一致性 Hash，相同参数的请求总是发到同一提供者
* ConfigurableWeight 权重可配置的负载均衡策略

### 容错策略

Motan 在集群调用失败时，提供了两种容错方案，并支持自定义扩展。 高可用集群容错策略在Client端生效，因此需在Client端添加配置 目前支持的集群容错策略有：

* Failover 失效切换（缺省） 失败自动切换，当出现失败，重试其它服务器。
* Failfast 快速失败 只发起一次调用，失败立即报错。

### 注册中心与服务发现

### 优雅的停止服务

Motan支持在Consul、ZooKeeper集群环境下优雅的关闭节点，当需要关闭或重启节点时，可以先将待上线节点从集群中摘除，避免直接关闭影响正常请求。

待关闭节点需要调用以下代码，建议通过servlet或业务的管理模块进行该调用。

```java
MotanSwitcherUtil.setSwitcherValue(MotanConstants.REGISTRY_HEARTBEAT_SWITCHER, false)
```



