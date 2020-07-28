# Microservice

# 一.Dubbo

## 单体架构

![](../media/pictures/Microservice.assets/be01386bf19f71fe8467bf20132bcc0c.png)

![](../media/pictures/Microservice.assets/d77c37dd3a3a108509e903211a14ff94.png)

### 优缺点

![](../media/pictures/Microservice.assets/391bfa438a9991af7f55b236c2a73e12.png)

修改后 测试麻烦

迭代困难

修改工具类，其他的模块都受到影响

某个模块扩展扩容起来麻烦

部署和回滚不方便

## 微服务架构引入

### 概念

微服务是指开发一个单个小型的但有业务功能的服务，每个服务都有自己的处理和轻量通讯机制，可以部署在单个或多个服务器上。微服务也指一种种松耦合的、有一定的有界上下文的面向服务架构。也就是说，如果每个服务都要同时修改，那么它们就不是微服务，因为它们紧耦合在一起；如果你需要掌握一个服务太多的上下文场景使用条件，那么它就是一个有上下文边界的服务。

### 架构图

![](../media/pictures/Microservice.assets/a5ed18885a7240334ad1b8cf16d6f785.png)

![](../media/pictures/Microservice.assets/4dc25fa09547d7d41812a63e195cfd2b.png)

### 微服务架构设计原则

拆分足够小

服务之间轻量级通信

### 微服务的优点

相对于单体架构，它的主要特点是**组件化、松耦合、自治、去中心化**，体现在以下几个方面：

一组小的服务
服务粒度要小，而每个服务是针对一个单一职责的业务能力的封装，专注做好一件事情。

独立部署运行和扩展

每个服务能够独立被部署并运行在一个进程内。这种运行和部署方式能够赋予系统灵活的代码组织方式和发布节奏，使得快速交付和应对变化成为可能。

独立开发和演化

技术选型灵活，不受遗留系统技术约束。合适的业务问题选择合适的技术可以独立演化。服务与服务之间采取与语言无关的API进行集成。相对单体架构，微服务架构是更面向业务创新的一种架构模式。

独立团队和自治

团队对服务的整个生命周期负责，工作在独立的上下文中，自己决策自己治理，而不需要统一的指挥中心。团队和团队之间通过松散的社区部落进行衔接。

### 微服务的缺点

服务拆分微服务架构可能带来过多的操作。

分布式系统可能复杂难以管理。

因为分布部署跟踪问题难。

分布式事务比较难处理

当服务数量增加，管理复杂性增加。

等

### 微服务拆分思路

#### 横向拆分

根据业务来拆分

![](../media/pictures/Microservice.assets/22e8dba61d1030921e6aed34169e2cdd.png)

#### 纵向拆分 

根据层次来拆分

![](../media/pictures/Microservice.assets/fb0154c9a3d57c61127dae4a3413f9db.png)

### 微服务的选择

下面两个就想当于自配电脑(Dubbo),和品牌电脑的关系(Springcloud)!

#### Dubbo （RPC）

##### Dubbo(这个是传输层协议 速度快)

Dubbo是阿里集团开源的一个极为出名的RPC框架，在很多互联网公司和企业应用中广泛使用。协议和序列化框架都可以插拔是及其鲜明的特色。同样的远程接口是基于Java Interface，并且依托于spring框架方便开发。可以方便的打包成单一文件，独立进程运行，和现在的微服务概念一致。所以目前Dubbo是一种广泛使用的微服务架构框架。

###### RPC 

RPC= Remote Process Call 跨进程调用

RPC的本质是提供了一种轻量无感知的跨进程通信的方式，在分布式机器上调用其他方法与本地调用无异（远程调用的过程是透明的，你并不知道这个调用的方法是部署在哪里，通过PRC能够解耦服务）。RPC是根据语言的API来定义的，而不是基于网络的应用来定义的，调用更方便，协议私密更安全、内容更小效率更高。

![](../media/pictures/Microservice.assets/ac8ff59370709f3755eec59630f93b2e.png)

客户端（Client），服务的调用方。

服务端（Server），真正的服务提供者。

客户端存根，存放服务端的地址消息，再将客户端的请求参数打包成网络消息，然后通过网络远程发送给服务方。

服务端存根，接收客户端发送过来的消息，将消息解包，并调用本地的方法。

基于TCP/IP协议。速度快。

![](../media/pictures/Microservice.assets/625f185c66747f68f35690b1f7757cc0.png)

#### Springcloud （HTTP）

##### Springcloud （HTTP/REST）(这个是应用层协议 速度慢 但是全 想当于品牌电脑)

Spring Cloud来源于Spring，利用Spring Boot进行快捷开发。 Spring
Cloud基本上都是使用了现有的开源框架进行的集成，学习的难度和部署的门槛就比较低，对于中小型企业来说，更易于使用和落地。Spring
Cloud
核心组件Eureka是Netflix开源的一款提供服务注册和发现的产品，它提供了完整的Service
Registry和Service Discovery实现。也是Spring Cloud体系中最重要最核心的组件之一。

#### http

**应用层协议**，简单。

http接口是在接口不多、系统与系统交互较少的情况下，解决信息孤岛初期常使用的一种通信手段；优点就是简单、直接、开发方便。利用现成的http协议
进行传输。

使用Http协议的微服务，通常返回json数据，然后把json转换为对象。

#### 小结

RPC服务和HTTP服务还是存在很多的不同点的，一般来说，RPC服务主要是针对大型企业的，而HTTP服务主要是针对小企业的，因为RPC效率更高，而HTTP服务开发迭代会更快。**总之，选用什么样的框架不是按照市场上流行什么而决定的，而是要对整个项目进行完整地评估。**

### 微服务的基本概念

#### 服务提供者Provider

提供服务的具体实现。

#### 服务调用者Consumer

通过一些框架来调用服务提供者提供的服务

注意：同一个微服务，既可以是provider，也可以是consumer。

### 拓展 阿里架构演变之路

https://segmentfault.com/a/1190000018626163  这是作者原来文章的链接!

下面是从源出处复制过来的!

#### 1. 概述

本文以淘宝作为例子，介绍从一百个并发到千万级并发情况下服务端的架构的演进过程，同时列举出每个演进阶段会遇到的相关技术，让大家对架构的演进有一个整体的认知，文章最后汇总了一些架构设计的原则。

#### 2. 基本概念

在介绍架构之前，为了避免部分读者对架构设计中的一些概念不了解，下面对几个最基础的概念进行介绍：

- **分布式**
  系统中的多个模块在不同服务器上部署，即可称为分布式系统，如Tomcat和数据库分别部署在不同的服务器上，或两个相同功能的Tomcat分别部署在不同服务器上
- **高可用**
  系统中部分节点失效时，其他节点能够接替它继续提供服务，则可认为系统具有高可用性
- **集群**
  一个特定领域的软件部署在多台服务器上并作为一个整体提供一类服务，这个整体称为集群。如Zookeeper中的Master和Slave分别部署在多台服务器上，共同组成一个整体提供集中配置服务。在常见的集群中，客户端往往能够连接任意一个节点获得服务，并且当集群中一个节点掉线时，其他节点往往能够自动的接替它继续提供服务，这时候说明集群具有高可用性
- **负载均衡**
  请求发送到系统时，通过某些方式把请求均匀分发到多个节点上，使系统中每个节点能够均匀的处理请求负载，则可认为系统是负载均衡的
- **正向代理和反向代理**
  系统内部要访问外部网络时，统一通过一个代理服务器把请求转发出去，在外部网络看来就是代理服务器发起的访问，此时代理服务器实现的是正向代理；当外部请求进入系统时，代理服务器把该请求转发到系统中的某台服务器上，对外部请求来说，与之交互的只有代理服务器，此时代理服务器实现的是反向代理。简单来说，正向代理是代理服务器代替系统内部来访问外部网络的过程，反向代理是外部请求访问系统时通过代理服务器转发到内部服务器的过程。

#### 3. 架构演进

##### 3.1 单机架构

![clipboard.png](../media/pictures/Microservice.assets/2664959638-5ca02e1d2e99b_articlex.png)

以淘宝作为例子。在网站最初时，应用数量与用户数都较少，可以把Tomcat和数据库部署在同一台服务器上。浏览器往www.taobao.com发起请求时，首先经过DNS服务器（域名系统）把域名转换为实际IP地址10.102.4.1，浏览器转而访问该IP对应的Tomcat。

> **随着用户数的增长，Tomcat和数据库之间竞争资源，单机性能不足以支撑业务**

##### 3.2 第一次演进：Tomcat与数据库分开部署

![clipboard.png](../media/pictures/Microservice.assets/2571350918-5ca02dfbdc242_articlex.png)

Tomcat和数据库分别独占服务器资源，显著提高两者各自性能。

> **随着用户数的增长，并发读写数据库成为瓶颈**

##### 3.3 第二次演进：引入本地缓存和分布式缓存

![clipboard.png](../media/pictures/Microservice.assets/1088865837-5ca031313f044_articlex.png)

在Tomcat同服务器上或同JVM中增加本地缓存，并在外部增加分布式缓存，缓存热门商品信息或热门商品的html页面等。通过缓存能把绝大多数请求在读写数据库前拦截掉，大大降低数据库压力。其中涉及的技术包括：使用memcached作为本地缓存，使用Redis作为分布式缓存，还会涉及缓存一致性、缓存穿透/击穿、缓存雪崩、热点数据集中失效等问题。

> **缓存抗住了大部分的访问请求，随着用户数的增长，并发压力主要落在单机的Tomcat上，响应逐渐变慢**

##### 3.4 第三次演进：引入反向代理实现负载均衡

![clipboard.png](../media/pictures/Microservice.assets/2872647211-5c95fef4928ad_articlex.png)

在多台服务器上分别部署Tomcat，使用反向代理软件（Nginx）把请求均匀分发到每个Tomcat中。此处假设Tomcat最多支持100个并发，Nginx最多支持50000个并发，那么理论上Nginx把请求分发到500个Tomcat上，就能抗住50000个并发。其中涉及的技术包括：Nginx、HAProxy，两者都是工作在网络第七层的反向代理软件，主要支持http协议，还会涉及session共享、文件上传下载的问题。

> **反向代理使应用服务器可支持的并发量大大增加，但并发量的增长也意味着更多请求穿透到数据库，单机的数据库最终成为瓶颈**

##### 3.5 第四次演进：数据库读写分离

![clipboard.png](../media/pictures/Microservice.assets/1589885053-5c96032e3c356_articlex.png)

把数据库划分为读库和写库，读库可以有多个，通过同步机制把写库的数据同步到读库，对于需要查询最新写入数据场景，可通过在缓存中多写一份，通过缓存获得最新数据。其中涉及的技术包括：Mycat，它是数据库中间件，可通过它来组织数据库的分离读写和分库分表，客户端通过它来访问下层数据库，还会涉及数据同步，数据一致性的问题。

> **业务逐渐变多，不同业务之间的访问量差距较大，不同业务直接竞争数据库，相互影响性能**

##### 3.6 第五次演进：数据库按业务分库

![clipboard.png](../media/pictures/Microservice.assets/250737400-5c9653d44e54e_articlex.png)

把不同业务的数据保存到不同的数据库中，使业务之间的资源竞争降低，对于访问量大的业务，可以部署更多的服务器来支撑。这样同时导致跨业务的表无法直接做关联分析，需要通过其他途径来解决，但这不是本文讨论的重点，有兴趣的可以自行搜索解决方案。

> **随着用户数的增长，单机的写库会逐渐会达到性能瓶颈**

##### 3.7 第六次演进：把大表拆分为小表

![clipboard.png](../media/pictures/Microservice.assets/111902257-5c960f793734f_articlex.png)

比如针对评论数据，可按照商品ID进行hash，路由到对应的表中存储；针对支付记录，可按照小时创建表，每个小时表继续拆分为小表，使用用户ID或记录编号来路由数据。只要实时操作的表数据量足够小，请求能够足够均匀的分发到多台服务器上的小表，那数据库就能通过水平扩展的方式来提高性能。其中前面提到的Mycat也支持在大表拆分为小表情况下的访问控制。

这种做法显著的增加了数据库运维的难度，对DBA的要求较高。数据库设计到这种结构时，已经可以称为分布式数据库，但是这只是一个逻辑的数据库整体，数据库里不同的组成部分是由不同的组件单独来实现的，如分库分表的管理和请求分发，由Mycat实现，SQL的解析由单机的数据库实现，读写分离可能由网关和消息队列来实现，查询结果的汇总可能由数据库接口层来实现等等，这种架构其实是MPP（大规模并行处理）架构的一类实现。

目前开源和商用都已经有不少MPP数据库，开源中比较流行的有Greenplum、TiDB、Postgresql XC、HAWQ等，商用的如南大通用的GBase、睿帆科技的雪球DB、华为的LibrA等等，不同的MPP数据库的侧重点也不一样，如TiDB更侧重于分布式OLTP场景，Greenplum更侧重于分布式OLAP场景，这些MPP数据库基本都提供了类似Postgresql、Oracle、MySQL那样的SQL标准支持能力，能把一个查询解析为分布式的执行计划分发到每台机器上并行执行，最终由数据库本身汇总数据进行返回，也提供了诸如权限管理、分库分表、事务、数据副本等能力，并且大多能够支持100个节点以上的集群，大大降低了数据库运维的成本，并且使数据库也能够实现水平扩展。

> **数据库和Tomcat都能够水平扩展，可支撑的并发大幅提高，随着用户数的增长，最终单机的Nginx会成为瓶颈**

##### 3.8 第七次演进：使用LVS或F5来使多个Nginx负载均衡

![clipboard.png](../media/pictures/Microservice.assets/1157555056-5c965af7a8de0_articlex.png)

由于瓶颈在Nginx，因此无法通过两层的Nginx来实现多个Nginx的负载均衡。图中的LVS和F5是工作在网络第四层的负载均衡解决方案，其中LVS是软件，运行在操作系统内核态，可对TCP请求或更高层级的网络协议进行转发，因此支持的协议更丰富，并且性能也远高于Nginx，可假设单机的LVS可支持几十万个并发的请求转发；F5是一种负载均衡硬件，与LVS提供的能力类似，性能比LVS更高，但价格昂贵。由于LVS是单机版的软件，若LVS所在服务器宕机则会导致整个后端系统都无法访问，因此需要有备用节点。可使用keepalived软件模拟出虚拟IP，然后把虚拟IP绑定到多台LVS服务器上，浏览器访问虚拟IP时，会被路由器重定向到真实的LVS服务器，当主LVS服务器宕机时，keepalived软件会自动更新路由器中的路由表，把虚拟IP重定向到另外一台正常的LVS服务器，从而达到LVS服务器高可用的效果。

此处需要注意的是，上图中从Nginx层到Tomcat层这样画并不代表全部Nginx都转发请求到全部的Tomcat，在实际使用时，可能会是几个Nginx下面接一部分的Tomcat，这些Nginx之间通过keepalived实现高可用，其他的Nginx接另外的Tomcat，这样可接入的Tomcat数量就能成倍的增加。

> **由于LVS也是单机的，随着并发数增长到几十万时，LVS服务器最终会达到瓶颈，此时用户数达到千万甚至上亿级别，用户分布在不同的地区，与服务器机房距离不同，导致了访问的延迟会明显不同**

##### 3.9 第八次演进：通过DNS轮询实现机房间的负载均衡

![clipboard.png](../media/pictures/Microservice.assets/1896228394-5c9662ac87756_articlex.png)

在DNS服务器中可配置一个域名对应多个IP地址，每个IP地址对应到不同的机房里的虚拟IP。当用户访问www.taobao.com时，DNS服务器会使用轮询策略或其他策略，来选择某个IP供用户访问。此方式能实现机房间的负载均衡，至此，系统可做到机房级别的水平扩展，千万级到亿级的并发量都可通过增加机房来解决，系统入口处的请求并发量不再是问题。

> **随着数据的丰富程度和业务的发展，检索、分析等需求越来越丰富，单单依靠数据库无法解决如此丰富的需求**

##### 3.10 第九次演进：引入NoSQL数据库和搜索引擎等技术

![clipboard.png](../media/pictures/Microservice.assets/1190021994-5ca03c930e572_articlex.png)

当数据库中的数据多到一定规模时，数据库就不适用于复杂的查询了，往往只能满足普通查询的场景。对于统计报表场景，在数据量大时不一定能跑出结果，而且在跑复杂查询时会导致其他查询变慢，对于全文检索、可变数据结构等场景，数据库天生不适用。因此需要针对特定的场景，引入合适的解决方案。如对于海量文件存储，可通过分布式文件系统HDFS解决，对于key value类型的数据，可通过HBase和Redis等方案解决，对于全文检索场景，可通过搜索引擎如ElasticSearch解决，对于多维分析场景，可通过Kylin或Druid等方案解决。

当然，引入更多组件同时会提高系统的复杂度，不同的组件保存的数据需要同步，需要考虑一致性的问题，需要有更多的运维手段来管理这些组件等。

> **引入更多组件解决了丰富的需求，业务维度能够极大扩充，随之而来的是一个应用中包含了太多的业务代码，业务的升级迭代变得困难**

##### 3.11 第十次演进：大应用拆分为小应用

![clipboard.png](../media/pictures/Microservice.assets/1992263855-5ca04d46dd717_articlex.png)

按照业务板块来划分应用代码，使单个应用的职责更清晰，相互之间可以做到独立升级迭代。这时候应用之间可能会涉及到一些公共配置，可以通过分布式配置中心Zookeeper来解决。

> **不同应用之间存在共用的模块，由应用单独管理会导致相同代码存在多份，导致公共功能升级时全部应用代码都要跟着升级**

3.12 第十一次演进：复用的功能抽离成微服务

![clipboard.png](../media/pictures/Microservice.assets/651851067-5ca04fe08f7ee_articlex.png)

如用户管理、订单、支付、鉴权等功能在多个应用中都存在，那么可以把这些功能的代码单独抽取出来形成一个单独的服务来管理，这样的服务就是所谓的微服务，应用和服务之间通过HTTP、TCP或RPC请求等多种方式来访问公共服务，每个单独的服务都可以由单独的团队来管理。此外，可以通过Dubbo、SpringCloud等框架实现服务治理、限流、熔断、降级等功能，提高服务的稳定性和可用性。

> **不同服务的接口访问方式不同，应用代码需要适配多种访问方式才能使用服务，此外，应用访问服务，服务之间也可能相互访问，调用链将会变得非常复杂，逻辑变得混乱**

##### 3.13 第十二次演进：引入企业服务总线ESB屏蔽服务接口的访问差异

![clipboard.png](../media/pictures/Microservice.assets/1162448692-5ca052a998911_articlex.png)

通过ESB统一进行访问协议转换，应用统一通过ESB来访问后端服务，服务与服务之间也通过ESB来相互调用，以此降低系统的耦合程度。这种单个应用拆分为多个应用，公共服务单独抽取出来来管理，并使用企业消息总线来解除服务之间耦合问题的架构，就是所谓的SOA（面向服务）架构，这种架构与微服务架构容易混淆，因为表现形式十分相似。个人理解，微服务架构更多是指把系统里的公共服务抽取出来单独运维管理的思想，而SOA架构则是指一种拆分服务并使服务接口访问变得统一的架构思想，SOA架构中包含了微服务的思想。

> **业务不断发展，应用和服务都会不断变多，应用和服务的部署变得复杂，同一台服务器上部署多个服务还要解决运行环境冲突的问题，此外，对于如大促这类需要动态扩缩容的场景，需要水平扩展服务的性能，就需要在新增的服务上准备运行环境，部署服务等，运维将变得十分困难**

##### 3.14 第十三次演进：引入容器化技术实现运行环境隔离与动态服务管理

![clipboard.png](../media/pictures/Microservice.assets/2760745238-5ca055e4b20a9_articlex.png)

目前最流行的容器化技术是Docker，最流行的容器管理服务是Kubernetes(K8S)，应用/服务可以打包为Docker镜像，通过K8S来动态分发和部署镜像。Docker镜像可理解为一个能运行你的应用/服务的最小的操作系统，里面放着应用/服务的运行代码，运行环境根据实际的需要设置好。把整个“操作系统”打包为一个镜像后，就可以分发到需要部署相关服务的机器上，直接启动Docker镜像就可以把服务起起来，使服务的部署和运维变得简单。

在大促的之前，可以在现有的机器集群上划分出服务器来启动Docker镜像，增强服务的性能，大促过后就可以关闭镜像，对机器上的其他服务不造成影响（在3.14节之前，服务运行在新增机器上需要修改系统配置来适配服务，这会导致机器上其他服务需要的运行环境被破坏）。

> **使用容器化技术后服务动态扩缩容问题得以解决，但是机器还是需要公司自身来管理，在非大促的时候，还是需要闲置着大量的机器资源来应对大促，机器自身成本和运维成本都极高，资源利用率低**

##### 3.15 第十四次演进：以云平台承载系统

![clipboard.png](../media/pictures/Microservice.assets/1409345676-5ca05cae06402_articlex.png)

系统可部署到公有云上，利用公有云的海量机器资源，解决动态硬件资源的问题，在大促的时间段里，在云平台中临时申请更多的资源，结合Docker和K8S来快速部署服务，在大促结束后释放资源，真正做到按需付费，资源利用率大大提高，同时大大降低了运维成本。

所谓的云平台，就是把海量机器资源，通过统一的资源管理，抽象为一个资源整体，在之上可按需动态申请硬件资源（如CPU、内存、网络等），并且之上提供通用的操作系统，提供常用的技术组件（如Hadoop技术栈，MPP数据库等）供用户使用，甚至提供开发好的应用，用户不需要关系应用内部使用了什么技术，就能够解决需求（如音视频转码服务、邮件服务、个人博客等）。在云平台中会涉及如下几个概念：

- **IaaS：**基础设施即服务。对应于上面所说的机器资源统一为资源整体，可动态申请硬件资源的层面；
- **PaaS：**平台即服务。对应于上面所说的提供常用的技术组件方便系统的开发和维护；
- **SaaS：**软件即服务。对应于上面所说的提供开发好的应用或服务，按功能或性能要求付费。

> **至此，以上所提到的从高并发访问问题，到服务的架构和系统实施的层面都有了各自的解决方案，但同时也应该意识到，在上面的介绍中，其实是有意忽略了诸如跨机房数据同步、分布式事务实现等等的实际问题，这些问题以后有机会再拿出来单独讨论**

#### 4. 架构设计总结

- **架构的调整是否必须按照上述演变路径进行？**
  不是的，以上所说的架构演变顺序只是针对某个侧面进行单独的改进，在实际场景中，可能同一时间会有几个问题需要解决，或者可能先达到瓶颈的是另外的方面，这时候就应该按照实际问题实际解决。如在政府类的并发量可能不大，但业务可能很丰富的场景，高并发就不是重点解决的问题，此时优先需要的可能会是丰富需求的解决方案。
- **对于将要实施的系统，架构应该设计到什么程度？**
  对于单次实施并且性能指标明确的系统，架构设计到能够支持系统的性能指标要求就足够了，但要留有扩展架构的接口以便不备之需。对于不断发展的系统，如电商平台，应设计到能满足下一阶段用户量和性能指标要求的程度，并根据业务的增长不断的迭代升级架构，以支持更高的并发和更丰富的业务。
- **服务端架构和大数据架构有什么区别？**
  所谓的“大数据”其实是海量数据采集清洗转换、数据存储、数据分析、数据服务等场景解决方案的一个统称，在每一个场景都包含了多种可选的技术，如数据采集有Flume、Sqoop、Kettle等，数据存储有分布式文件系统HDFS、FastDFS，NoSQL数据库HBase、MongoDB等，数据分析有Spark技术栈、机器学习算法等。总的来说大数据架构就是根据业务的需求，整合各种大数据组件组合而成的架构，一般会提供分布式存储、分布式计算、多维分析、数据仓库、机器学习算法等能力。而服务端架构更多指的是应用组织层面的架构，底层能力往往是由大数据架构来提供。
- **有没有一些架构设计的原则？**
  - N+1设计。系统中的每个组件都应做到没有单点故障；
  - 回滚设计。确保系统可以向前兼容，在系统升级时应能有办法回滚版本；
  - 禁用设计。应该提供控制具体功能是否可用的配置，在系统出现故障时能够快速下线功能；
  - 监控设计。在设计阶段就要考虑监控的手段；
  - 多活数据中心设计。若系统需要极高的高可用，应考虑在多地实施数据中心进行多活，至少在一个机房断电的情况下系统依然可用；
  - 采用成熟的技术。刚开发的或开源的技术往往存在很多隐藏的bug，出了问题没有商业支持可能会是一个灾难；
  - 资源隔离设计。应避免单一业务占用全部资源；
  - 架构应能水平扩展。系统只有做到能水平扩展，才能有效避免瓶颈问题；
  - 非核心则购买。非核心功能若需要占用大量的研发资源才能解决，则考虑购买成熟的产品；
  - 使用商用硬件。商用硬件能有效降低硬件故障的机率；
  - 快速迭代。系统应该快速开发小功能模块，尽快上线进行验证，早日发现问题大大降低系统交付的风险；
  - 无状态设计。服务接口应该做成无状态的，当前接口的访问不依赖于接口上次访问的状态。

## Dubbo引入

### Dubbo介绍

<http://dubbo.apache.org/en-us/>

### Spring和Dubbo的结合

#### 入门案例

参考文档：<https://dubbo.gitbooks.io/dubbo-user-book/content/quick-start.html>

##### 导包

见资料。

##### 服务提供者 

##### 代码

首先我们在服务端定义一个接口

![](../media/pictures/Microservice.assets/1ddc209e6ef6a524024997bc53ca3cf1.png)

然后我在服务端提供这个接口的实现

![](../media/pictures/Microservice.assets/6a7c6b3b2755feb69455529e8497395b.png)

##### 配置

![](../media/pictures/Microservice.assets/fa1e3e4cc8f504c746e87a1e01ce7286.png)

##### 服务器使用者 

###### 代码

![](../media/pictures/Microservice.assets/4f4062b2cf24f0b5389881f84d0ad11e.png)

远程调用代码

![](../media/pictures/Microservice.assets/2ce43942af3f1ff23b44b75314bfd3af.png)

###### 配置

![](../media/pictures/Microservice.assets/32a3c0f74c325ec723440dcc369cd82c.png)

##### 测试结果

![](../media/pictures/Microservice.assets/26954a843fb9f74e9cde7c16c19902e4.png)



**这里需要注意的是,这里服务的提供者和服务的消费者名字要一样,不光是接口和类的名字一样,而且包名也要一样!**

![1570800056119](../media/pictures/Microservice.assets/1570800056119.png)

这里的两个接口必须要一样!

### 架构

![1570802882355](../media/pictures/Microservice.assets/1570802882355.png)

#### 第一种方式直连!相当于没有上面注册!

#### 第二种方式用注册中心中的zookepper!

zookepper使用,首先减压!

然后进去目录中,将文件名字修改:

![1570803035936](../media/pictures/Microservice.assets/1570803035936.png)

因为启动以后会默认找zoo.cfg这个文件!



然后需要启动这的zookeeper,这里需要注意的是,路径不能有中文,目录如果放的太深,或者路径中有其他奇怪字符,这个是运行不了的,会一直报错,提示找不到主类!

![1570804540341](../media/pictures/Microservice.assets/1570804540341.png)

![1570804910045](../media/pictures/Microservice.assets/1570804910045.png)

这样就启动成功啦!

这其中遇到一个问题,问题详细信息看error18!

zookeeper会受电脑广播和其他东西的影响!

而且在wins环境下,会运行不稳定!有时候需要耐心一定!

![1570870852064](../media/pictures/Microservice.assets/1570870852064.png)

出现这个,就意味着成功啦!



#### 入门案例分析

### SpringBoot 和 Dubbo的结合

参考文档<https://github.com/alibaba/dubbo-spring-boot-starter>



首先需要导一个包!springboot对dubbo的支持包!上面是github的地址!

#### 导包

```xml
<dependency>
    <groupId>com.alibaba.spring.boot</groupId>
    <artifactId>dubbo-spring-boot-starter</artifactId>
    <version>2.0.0</version>
</dependency>
```

Springboot约定大于配置,官方文档中没有配置端口,其实是默认配置了端口,只要不修改端口,默认就是

```xml
spring.application.name=dubbo-spring-boot-starter
spring.dubbo.server=true
spring.dubbo.registry=N/A
```





#### 提供者

![](../media/pictures/Microservice.assets/f0e79697c6c1d5415d3c878f84d3b34c.png)

**注意:这里的Service是dubbo中的!要注意!**

使用之前要导包!

![](../media/pictures/Microservice.assets/04c8cb6e6104504c76086b191c682e19.png)

配置：

```java
spring.application.name=dubbo-spring-boot-starter
spring.dubbo.protocol.name=dubbo
spring.dubbo.protocol.port=20880
spring.dubbo.server=true
spring.dubbo.registry=N/A
```



#### 使用者

也要实现一模一样的接口！

![](../media/pictures/Microservice.assets/ffd1647ad2a27e2a3cbd4bd9fd668ce0.png)

![](../media/pictures/Microservice.assets/1e3adc3901c569b59d50e303575ef8a3.png)

然后在main方法里测试！

**注意**:这里要开启功能,需要上面的注解

```java
@EnableDubboConfiguraion
```

![](../media/pictures/Microservice.assets/8d9f3596a9273968defb166629b682bb.png)

#### 测试

先启动服务提供者：

![](../media/pictures/Microservice.assets/7131d4fb96a772e2ce12dc39c84e0718.png)

在启动使用者：

这行log出现在下面的空行位置

![](../media/pictures/Microservice.assets/167a3119d6eb87a271d3708cb48dcc61.png)

![](../media/pictures/Microservice.assets/c7e6d9f38b4ef5eb42001a8ef20f3560.png)



在老师上课的dome中,老师使用了一个公共包common,公共包里面的pom.xml配置,要写成

```xml
<packaging>jar</packaging>
```

公共包里面建放了DemoService接口,那么下面两个中就没有必要放这个接口啦!

但是要导入上面的common包!

```xml
<!--要引入common包里面的包,这里需要引入common包-->
<dependency>
    <groupId>com.cskaoyan</groupId>
    <artifactId>common</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

这样,下面两个包就可以使用common里面的包啦!

这种导入一个公共包的做法,不容易犯错!



公共类中导入一个依赖,然后下面两个包中都是可以使用的!

![1570882252588](../media/pictures/Microservice.assets/1570882252588.png)

```xml
<!--这个依赖狭下面两个都需要!-->
<dependency>
    <groupId>com.alibaba.spring.boot</groupId>
    <artifactId>dubbo-spring-boot-starter</artifactId>
    <version>2.0.0</version>
</dependency>
```

这里可以看到下面两个包中已经包含了上面包中的,已经包含了公共包中的依赖!

上面的是直连

如果想让项目变成需要注册的,还需要导入zookeeper

```xml
<!--这个是导入zookeeper的包-->
<dependency>
	<groupId>com.101tec</groupId>
	<artifactId>zkclient</artifactId>
	<version>0.10</version>
</dependency>
```





### 直连提供者

#### 介绍

我们刚才使用的微服务的用法，实际上是一种最简单的点对点调用方式。这种方式通常用于测试环境。

在开发及测试环境下，经常需要绕过注册中心，只测试指定服务提供者，这时候可能需要点对点直连，点对点直联方式，将以服务接口为单位，忽略注册中心的提供者列表，A
接口配置点对点，不影响 B 接口从注册中心获取列表。

![](../media/pictures/Microservice.assets/15adcb224fcef4191f9106fd36f62105.png)

**注意** 为了避免复杂化线上环境，不要在线上使用这个功能，只应在测试阶段使用。

#### 弊端

不利于分布式的扩展

### 服务注册和服务发现

#### 架构图

这里是长连接!长连接最主要的特点是建立心跳连接!过一会会发射一些数据!

![](../media/pictures/Microservice.assets/acc8b5168c63f753c642f845b11de339.png)

名词解释：

![](../media/pictures/Microservice.assets/116873b8f0e64756d54775a4b40c1d82.png)

### ZooKeeper

是一个中间件，负责为分布式系统提供协调服务。服务注册和服务发现。

<https://www.apache.org/dyn/closer.cgi/zookeeper/>

下载路径

下载解压之后

修改一个文件名

zoo_sample.cfg修改为

![](../media/pictures/Microservice.assets/ec83dfc5f99bf5219216aa4f80d1e1c4.png)

启动：

![](../media/pictures/Microservice.assets/730080cbd8e58d9bde067d8b0903a607.png)

![](../media/pictures/Microservice.assets/5bb55b0b35a442e2882accb51ad945dd.png)

### Spring +dubbo项目 如何整合zookeeper

#### 导入依赖

\<dependency\>  
\<groupId\>com.101tec\</groupId\>  
\<artifactId\>zkclient\</artifactId\>  
\<version\>0.9\</version\>  
\</dependency\>  
\<dependency\>  
\<groupId\>org.apache.zookeeper\</groupId\>  
\<artifactId\>zookeeper\</artifactId\>  
\<version\>3.4.9\</version\>  
\<type\>pom\</type\>  
\</dependency\>

#### 修改服务端

![](../media/pictures/Microservice.assets/5af9e605d5751eec4aa074727bdb3d79.png)

启动：

没有报错，

Zookeeper那边的命令行会出现一些log

![](../media/pictures/Microservice.assets/8641ddc536193a03a16a54f50d9e2405.png)

#### 修改客户端

![](../media/pictures/Microservice.assets/a2e28d69a76f38bb32409e87c3202c2f.png)

#### 测试

![](../media/pictures/Microservice.assets/0cb2e6a8664c7ac126ba073055ea1d98.png)

![](../media/pictures/Microservice.assets/4af8d78e7df99c245100ea374eb7b2e3.png)

### Springboot 和 dubbo项目整合zookeeper

#### 服务端

增加了依赖

![](../media/pictures/Microservice.assets/bb743b6f6d742f4917a9d8d8c19cdc70.png)

修改地址：

spring.application.name=dubbo-spring-boot-starter  
spring.dubbo.server=true  
spring.dubbo.registry=zookeeper://localhost:2181

启动

#### 使用端

\<dependency\>  
\<groupId\>com.101tec\</groupId\>  
\<artifactId\>zkclient\</artifactId\>  
\<version\>0.10\</version\>  
\</dependency\>

配置文件：

增加如下：

spring.dubbo.registry=zookeeper://localhost:2181

代码里：

![](../media/pictures/Microservice.assets/125b23e796ba24d0e683d687662d5e94.png)

#### 测试

![](../media/pictures/Microservice.assets/11c12babf9fd43b68454fbb9403ec29e.png)

这里有一个面试题:

加入zookeeper挂掉以后,Dubbo还能不能正常调用??

可正常调用!因为本地有缓存!

![1570885788370](../media/pictures/Microservice.assets/1570885788370.png)









## Dubbo负载均衡

### 概念

LoadBalance
中文意思为负载均衡，它的职责是将网络请求，或者其他形式的负载“均摊”到不同的机器上。避免集群中部分服务器压力过大，而另一些服务器比较空闲的情况。通过负载均衡，可以让每台服务器获取到适合自己处理能力的负载。在为高负载服务器分流的同时，还可以避免资源浪费，一举两得。

### 负载均衡策略

![](../media/pictures/Microservice.assets/dd06bd3a7e584111a4c8a408e78ddba4.png)

#### Random

随机加权

RandomLoadBalance
是加权随机算法的具体实现，它的算法思想很简单。假设我们有一组服务器 servers = [A,
B, C]，他们对应的权重为 weights = [5, 3,
2]，权重总和为10。现在把这些权重值平铺在一维坐标值上，[0, 5) 区间属于服务器
A，[5, 8) 区间属于服务器 B，[8, 10) 区间属于服务器
C。接下来通过随机数生成器生成一个范围在 [0, 10)
之间的随机数，然后计算这个随机数会落到哪个区间上。权重越大的机器，在坐标轴上对应的区间范围就越大，因此随机数生成器生成的数字就会有更大的概率落到此区间内。

#### RoundRobin

我们有三台服务器 A、B、C。我们将第一个请求分配给服务器 A，第二个请求分配给服务器
B，第三个请求分配给服务器 C，第四个请求再次分配给服务器 A。这个过程就叫做

轮询。轮询是一种无状态负载均衡算法，实现简单，适用于每台服务器性能相近的场景下。

通常我们可以给轮询的机器设置不同的权重，经过加权后，每台服务器能够得到的请求数比例，接近或等于他们的权重比。比如服务器
A、B、C 权重比为 5:2:1。那么在8次请求中，服务器 A 将收到其中的5次请求，服务器 B
会收到其中的2次请求，服务器 C 则收到其中的1次请求。

#### LeastActive

LeastActiveLoadBalance
翻译过来是最小活跃数负载均衡。活跃调用数越小，表明该服务提供者效率越高，单位时间内可处理更多的请求。此时应优先将请求分配给该服务提供者。在具体实现中，每个服务提供者对应一个活跃数
active。初始情况下，所有服务提供者活跃数均为0。每收到一个请求，活跃数加1，完成请求后则将活跃数减1。在服务运行一段时间后，性能好的服务提供者处理请求的速度更快，因此活跃数下降的也越快，此时这样的服务提供者能够优先获取到新的服务请求、这就是最小活跃数负载均衡算法的基本思想。

#### ConsistentHash

![](../media/pictures/Microservice.assets/ea1e741ce818c1e439ab913c4c84e620.png)

### 配置

#### Random

默认配置

#### RoundRobin

##### 客户端配置

客户端服务级别

![](../media/pictures/Microservice.assets/a4a494abc4050b987ef6ff9c37134c69.png)

该服务的所有方法都使用roundrobin负载均衡。

客户端方法级别

![](../media/pictures/Microservice.assets/118ad755da8147dcf95f19aa62dd18ff.png)

如

![](../media/pictures/Microservice.assets/127a68ffe191362a99e5221b6d4e0c97.png)

只有该服务的hello方法使用roundrobin负载均衡。

##### 服务端配置

服务端服务级别

![](../media/pictures/Microservice.assets/57a0844a42642946790e94fe6b33e488.png)

该服务的所有方法都使用roundrobin负载均衡。

服务端方法级别

![](../media/pictures/Microservice.assets/27e77f44be552ada54ffea71bdfd543e.png)

只有该服务的该方法使用roundrobin负载均衡。

#### LeastActive

##### 补充说明

和Dubbo其他的配置类似，多个配置是有覆盖关系的：

1. 方法级优先，接口级次之，全局配置再次之。
2. 如果级别一样，则消费方优先，提供方次之。

所以，上面4种配置的优先级是:

1. 客户端方法级别配置。
2. 客户端接口级别配置。
3. 服务端方法级别配置。
4. 服务端接口级别配置。

## 补充说明

#### 启动检查

后面的check = false 就是启动检查!

```java
@Component
public class ThirdService {

    //这句话相当于 url = "dubbo://localhost:20880"
    @Reference(interfaceClass = DemoService.class,check = false)
    DemoService demoService;

    public String sendMsg(String msg){
        return demoService.sendMsg(msg);
    }
}
```

启动检查加了以后,我们不关心现在有没有provider,他会去检查!

#### Dubbo的特性





# 2.Guns

## Guns介绍

### 介绍

<https://gitee.com/naan1993/guns/>

- 快速构建应用系统（后台管理系统）。
- 默认提供了诸多业务系统的基本功能
- 继承了很多优秀的开源框架（开源）
- 可以直接作为一个后台管理系统的脚手架!

### 基本概念

![](../media/pictures/Microservice.assets/8f6c780959c4b54d2f2ba4678e912817.png)

### 基本使用 

这里开始搭建后台开发的架子。

#### 导入guns到IDEA

![](../media/pictures/Microservice.assets/dab02c1d9a41b181d8710bc7ce9a6ae7.png)

#### 如何启动guns项目

##### 运行admin模块

![](../media/pictures/Microservice.assets/a178f9aaf032b2830966f554dcd3a43c.png)

如何修改数据源？

在Guns-admin模块里 ，有个 配置文件 application.yml

里面默认的数据源配置如下：

![](../media/pictures/Microservice.assets/07619108db87df25f185a18013636026.png)

修改成我们自己的：

![](../media/pictures/Microservice.assets/89ede97f1c1d1fcdf78d604efd72cb1d.png)

**spring:**  
**profiles:** local  
**datasource:**  
**url:**
jdbc:mysql://127.0.0.1:3306/guns?autoReconnect=true&useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=UTC  
**username:** root  
**password:** 123456  
**db-name:** guns *\#用来搜集数据库的所有表*  
**filters:** wall,mergeStat

然后启动项目：

**登录 用户名 admin 密码 111111 可以成功登录！**

项目启动成功！



#### 初始化rest项目 （开发主要使用）

新建guns-rest数据库和里面的表

修改guns-rest的配置文件

![](../media/pictures/Microservice.assets/4cb52dce8dcdca21462f7f9019c73659.png)

报错，因为我们的数据库是mysql8，所以有一个配置字段不一样。

Caused by: com.baomidou.mybatisplus.exceptions.MybatisPlusException: Error:
GlobalConfigUtils setMetaData Fail ! Cause:java.sql.SQLException: The connection
property 'zeroDateTimeBehavior' acceptable values are: 'CONVERT_TO_NULL',
'EXCEPTION' or 'ROUND'. The value 'convertToNull' is not acceptable.

把

zeroDateTimeBehavior=convertToNull

修改为

&zeroDateTimeBehavior=CONVERT_TO_NULL

去掉也可以额的

再次启动

缺少包：

![](../media/pictures/Microservice.assets/4ae2855b71fd5fa7c8a6ce98e97e5066.png)

导入一个包：

\<dependency\>  
\<groupId\>log4j\</groupId\>  
\<artifactId\>log4j\</artifactId\>  
\<version\>1.2.17\</version\>  
\</dependency\>

访问下测试链接

<http://localhost/auth?userName=admin&password=admin>

返回

**{**"randomKey": "51656p","token": "eyJhbGciOiJIUzUxMiJ9.eyJyYW5kb21LZXkiOiI1MTY1NnAiLCJzdWIiOiJhZG1pbiIsImV4cCI6MTU1NTgyNzI2NCwiaWF0IjoxNTU1MjIyNDY0fQ.xfwl_6937X8T2etvQq6dQLuYb6ezCu4iJsAP0ggWQxn-TRuSJdoUQz0I02z4yNtVKtJbNakMwEolPp_XrbR46w"**}**

说明rest项目启动 OK！

### Rest项目的讲解

#### Rest的使用场景

APP开发 后端

前后端分离项目 后端

#### Rest新的模块的生成

#### 工具的按装

Chrome浏览器的两个插件

RestLet ：类似PostMan，模拟浏览器发请求，跟后端进行交互

FeHelper：优化返回的Json的显示效果

#### 基本使用

我们在Rest模块里写一个Rest接口

![](../media/pictures/Microservice.assets/2a9bd7920f7813c110ef1a937fdaf30b.png)

测试：

![](../media/pictures/Microservice.assets/67ec53833e12374d957954c3881f6510.png)

如何解决呢？

临时的解决方案：

修改配置文件，关闭鉴权

![](../media/pictures/Microservice.assets/b1c3e2a952896cdd1b44ae24315b7253.png)

测试:

![](../media/pictures/Microservice.assets/abe0094bdc581e819951d987450a3cc4.png)

### Rest模块的代码生成

代码生成器 **注意 是在test下面** 

```java
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.InjectionConfig;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.converts.MySqlTypeConvert;
import com.baomidou.mybatisplus.generator.config.rules.DbColumnType;
import com.baomidou.mybatisplus.generator.config.rules.DbType;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;
import org.junit.Test;

import java.util.HashMap;
import java.util.Map;

/**
 * 实体生成
 *
 * @author fengshuonan
 * @date 2017-08-23 12:15
 */
public class EntityGenerator {

    @Test
    public void entityGenerator() {
        AutoGenerator mpg = new AutoGenerator();

        // 全局配置
        GlobalConfig gc = new GlobalConfig();
        gc.setOutputDir("D:\\16thworkspace\\workspace\\guns\\guns-rest\  \src\\main\\java");//这里写你自己的java目录
        gc.setFileOverride(true);//是否覆盖
        gc.setActiveRecord(true);
        gc.setEnableCache(false);// XML 二级缓存
        gc.setBaseResultMap(true);// XML ResultMap
        gc.setBaseColumnList(false);// XML columList
        gc.setAuthor("lanzhao");
        mpg.setGlobalConfig(gc);

        // 数据源配置
        DataSourceConfig dsc = new DataSourceConfig();
        dsc.setDbType(DbType.MYSQL);
        dsc.setTypeConvert(new MySqlTypeConvert() {
            // 自定义数据库表字段类型转换【可选】
            @Override
            public DbColumnType processTypeConvert(String fieldType) {
                return super.processTypeConvert(fieldType);
            }
        });
        
        dsc.setDriverName("com.mysql.jdbc.Driver");
        dsc.setUsername("root");
        dsc.setPassword("123456");
        dsc.setUrl("jdbc:mysql://127.0.0.1:3306/guns_rest?serverTimezone=GMT&characterEncoding=utf8");
        mpg.setDataSource(dsc);

        // 策略配置
        StrategyConfig strategy = new StrategyConfig();
        //strategy.setTablePrefix(new String[]{"_"});// 此处可以修改为您的表前缀
        strategy.setNaming(NamingStrategy.underline_to_camel);// 表名生成策略
        strategy.setInclude(new String[]{"mtime_film_t"});
        mpg.setStrategy(strategy);

        // 包配置
        PackageConfig pc = new PackageConfig();
        pc.setParent(null);
        pc.setEntity("com.stylefeng.guns.rest.common.persistence.model");
        pc.setMapper("com.stylefeng.guns.rest.common.persistence.dao");
        pc.setXml("com.stylefeng.guns.rest.common.persistence.dao.mapping");
        pc.setService("com.stylefeng.guns.rest.common.persistence.service");       //本项目没用，生成之后删掉
        pc.setServiceImpl("com.stylefeng.guns.rest.common.persistence.service.impl");   //本项目没用，生成之后删掉
        pc.setController("TTT");    //本项目没用，生成之后删掉
        mpg.setPackageInfo(pc);

        // 注入自定义配置，可以在 VM 中使用 cfg.abc 设置的值
        InjectionConfig cfg = new InjectionConfig() {
            @Override
            public void initMap() {
                Map<String, Object> map = new HashMap<>();
                map.put("abc", this.getConfig().getGlobalConfig().getAuthor() + "-mp");
                this.setMap(map);
            }
        };
        mpg.setCfg(cfg);

        // 执行生成
        mpg.execute();

        // 打印注入设置
        System.err.println(mpg.getCfg().getMap().get("abc"));
    }
}

```

生成工具的路径

![](../media/pictures/Microservice.assets/1495afee990ef5edce341497764f38ae.png)

步骤：

#### 第一步，准备数据

新建数据库和表。

##### 个性化配置

修改生成代码的输出路径

![](../media/pictures/Microservice.assets/571e012ddd402ef93dae007ba9589fb9.png)

修改作者

修改数据源配置：

![](../media/pictures/Microservice.assets/2b761916433447e02e3da361c8dc94e6.png)

修改生成策略 作用的表

![](../media/pictures/Microservice.assets/51fe4c42da71e48176d5ca19da87e283.png)

修改生成代码的包名：

![](../media/pictures/Microservice.assets/8a9851260dd0ecae0c618170f242ff13.png)

最后，右键执行测试用例代码：

![](../media/pictures/Microservice.assets/bd408a2b9d05020774f00010c52a9d9c.png)

成功：

![](../media/pictures/Microservice.assets/edadf78718f7c269dbcb13406ec29b03.png)

生成之后，注意

![](../media/pictures/Microservice.assets/24c31648ebc1e8930711fd2d3574c171.png)

这个如果没有放到指定的目录，而是放到modular目录里，项目启动的时候mapper无法自动生成实例，会报找不到实例的错误。

![](../media/pictures/Microservice.assets/a7db731855aaf8a42e32d6130bc9c215.png)

这里mapper不用自己写实现

然后写代码测试一个 从controller 到service，到dao，出入一个Product

如下：测试插入一个product：

![](../media/pictures/Microservice.assets/0766564067b558c3cdac95551d3d953a.png)

使用RestLet发请求

![](../media/pictures/Microservice.assets/dcc02d102b9eb1eaa70f932afaa399a8.png)

代码正确的话，可以看到，product已经插入到数据库，

同时返回响应报文：

![](../media/pictures/Microservice.assets/865681c44f921c699fdc928a19eb4a9e.png)

说明测试成功！

# 3.API网关

## API网关

### 介绍

API网关是一个服务器，是系统的唯一入口。从面向对象设计的角度看，它与外观模式类似。API网关封装了系统内部架构，为每个客户端提供一个定制的API。它可能还具有其它职责，如身份验证、监控、负载均衡、缓存、请求分片与管理、静态响应处理。  
API网关方式的核心要点是，所有的客户端和消费端都通过统一的网关接入微服务，在网关层处理所有的非业务功能。通常，网关也是提供REST/HTTP的访问API。服务端通过API-GW注册和管理服务。

### 架构图

![](../media/pictures/Microservice.assets/f20cc42b7e9a13f584f39ab87bdd02ce.png)

多入口

![](../media/pictures/Microservice.assets/412a0bf298b75f5ccd29d43c53426c1d.png)

### 初步实现 搭架子

先把之前的Gunsrest的module复制一个，作为一个rest模块的架子。

复制之后：

先到父工程去 增加子模块，

![](../media/pictures/Microservice.assets/4555e69fc2b8656871ef69a1da3097cc.png)

在到自己的模块去修改

![](../media/pictures/Microservice.assets/2a8076a9b4bb260775a7d40d71d222a6.png)

复制之后需要引入module，修改完之后，maven重新import这个项目就自动在了。

然后在模块设置改一些东西。

生成了自己的模块文件之后，当前模块里有两个，

![](../media/pictures/Microservice.assets/4a0dbe731faa86194e46031ef5df36f2.png)

原来copy的模块配置文件就可以删除掉了把下面的guns-rest.iml 可以删掉了。

![](../media/pictures/Microservice.assets/f5d603dd5304e5827ab7a95b6a5c1f7a.png)

### 引入Dubbo

#### 导包

\<dependency\>  
\<groupId\>com.alibaba.spring.boot\</groupId\>  
\<artifactId\>dubbo-spring-boot-starter\</artifactId\>  
\<version\>2.0.0\</version\>  
\</dependency\>

\<dependency\>  
\<groupId\>com.101tec\</groupId\>  
\<artifactId\>zkclient\</artifactId\>  
\<version\>0.10\</version\>  
\</dependency\>

#### 修改配置文件

![](../media/pictures/Microservice.assets/5df28bc9df4c9e48ef7fe21319ca30f3.png)

#### 启动类上增加注解

![](../media/pictures/Microservice.assets/60b2c5c4cf5cb7ac83a51b3a7cfddc62.png)

#### 添加测试代码

![](../media/pictures/Microservice.assets/fc0f480ef3e9e2d133c8418bc8aa5b2a.png)

#### 启动测试

启动zookeeper

## 项目平台整合API网关

### API 网关

我们的项目的架构如下

![](../media/pictures/Microservice.assets/8113cfa60b0ec87420404f95fc6c0126.png)

### 新建一个Rest模块，作为我们的API网关

### API网关集成Dubbo

### 抽离公共接口

#### 引入

回顾之前dubbo的案例。

Dubbo的服务端 和
使用端，为了保证rpc调用的可用性，必须声明一模一样的接口在两个模块里。这样到时候微服务的模块多了之后，会比较麻烦，维护起来也很难。修改起来要修改很多地方。

怎么办？

我们可以专门新建一个子工程，这个自工程的主要目的就是存放我们的业务接口，以及一些大家都需要用的一些模型。

然后各个模块需要使用的话，就统一依赖这个子工程。

#### 实现

新建一个单独的子模块，比如叫guns-api

我们把上面的这种情况下需要使用的api接口以及一些大家都需要引用的类放在这个模块里。

然后install到maven仓库，在其他的模块里添加它作为依赖即可！



注意:每一个guns框架中每一个mapper都继承了一个BaseMapper<User>,里面有一些对应的方法!因为这个里面没有对应的方法mapper.xml

但是这里只能用原来有的bean





# 5:Mybatis-plus 

idea中插件叫mybatisX

这个插件没有安装上!

大佬说,首先要让market加载出来,才可以搜索的!



舍友说,分页插件要和生成器生成的mapper , .xml等一起用!不能单独用!然后有时间试试!

**这个分页和逆向工程很像,wrapper后面的,下面代码不完整!然后看官方文档!**

```java
Page<SteveOrderInfo> page = new Page<>(steveOrder.getNewPage(),steveOrder.getPageSize());

 EntityWrapper<SteveOrderInfo> wrapper = new EntityWrapper<>();
wrapper.eq("user_id", userId);
  //根据当前登录人username获取订单信息
mapper.(page,wrapper)
```

## 分页 要试试使用!

## 条件构造器(EntityWrapper)：

以上基本的 CRUD 操作，我们仅仅需要继承一个 BaseMapper 即可实现大部分单表 CRUD 操作。BaseMapper 提供了多达 17 个方法供使用, 可以极其方便的实现单一、批量、分页等操作，极大的减少开发负担。但是mybatis-plus的强大不限于此，请看如下需求该如何处理：
**需求：**
我们需要分页查询 tb_employee 表中，年龄在 18~50 之间性别为男且姓名为 xx 的所有用户，这时候我们该如何实现上述需求呢？
**使用MyBatis :** 需要在 SQL 映射文件中编写带条件查询的 SQL,并用PageHelper 插件完成分页. 实现以上一个简单的需求，往往需要我们做很多重复单调的工作。
**使用MP:** 依旧不用编写 SQL 语句，MP 提供了功能强大的条件构造器 ------ EntityWrapper。

**接下来就直接看几个案例体会EntityWrapper的使用。**

**1、分页查询年龄在18 - 50且gender为0、姓名为tom的用户：**

```php
List<Employee> employees = emplopyeeDao.selectPage(new Page<Employee>(1,3),
     new EntityWrapper<Employee>()
        .between("age",18,50)
        .eq("gender",0)
        .eq("last_name","tom")
);
```

**注：**由此案例可知，分页查询和之前一样，new 一个page对象传入分页信息即可。至于分页条件，new 一个EntityWrapper对象，调用该对象的相关方法即可。between方法三个参数，分别是column、value1、value2，该方法表示column的值要在value1和value2之间；eq是equals的简写，该方法两个参数，column和value，表示column的值和value要相等。注意column是数据表对应的字段，而非实体类属性字段。

**2、查询gender为0且名字中带有老师、或者邮箱中带有a的用户：**

```php
List<Employee> employees = emplopyeeDao.selectList(
                new EntityWrapper<Employee>()
               .eq("gender",0)
               .like("last_name","老师")
                //.or()//和or new 区别不大
               .orNew()
               .like("email","a")
);
```

**注：**未说分页查询，所以用selectList即可，用EntityWrapper的like方法进行模糊查询，like方法就是指column的值包含value值，此处like方法就是查询last_name中包含“老师”字样的记录；“或者”用or或者orNew方法表示，这两个方法区别不大，用哪个都可以，可以通过控制台的sql语句自行感受其区别。

**3、查询gender为0，根据age排序，简单分页：**

```php
List<Employee> employees = emplopyeeDao.selectList(
                new EntityWrapper<Employee>()
                .eq("gender",0)
                .orderBy("age")//直接orderby 是升序，asc
                .last("desc limit 1,3")//在sql语句后面追加last里面的内容(改为降序，同时分页)
);
```

**注：**简单分页是指不用page对象进行分页。orderBy方法就是根据传入的column进行升序排序，若要降序，可以使用orderByDesc方法，也可以如案例中所示用last方法；last方法就是将last方法里面的value值追加到sql语句的后面，在该案例中，最后的sql语句就变为`select ······ order by desc limit 1, 3`，追加了`desc limit 1,3`所以可以进行降序排序和分页。

**4、分页查询年龄在18 - 50且gender为0、姓名为tom的用户：**
条件构造器除了EntityWrapper，还有Condition。用Condition来处理一下这个需求：

```php
 List<Employee> employees = emplopyeeDao.selectPage(
                new Page<Employee>(1,2),
                Condition.create()
                        .between("age",18,50)
                        .eq("gender","0")
 );
```

**注：**Condition和EntityWrapper的区别就是，创建条件构造器时，EntityWrapper是new出来的，而Condition是调create方法创建出来。

**5、根据条件更新：**

```java
@Test
public void testEntityWrapperUpdate(){
        Employee employee = new Employee();
        employee.setLastName("苍老师");
        employee.setEmail("cjk@sina.com");
        employee.setGender(0);
        emplopyeeDao.update(employee,
                new EntityWrapper<Employee>()
                .eq("last_name","tom")
                .eq("age",25)
        );
}
```

**注：**该案例表示把last_name为tom，age为25的所有用户的信息更新为employee中设置的信息。

**6、根据条件删除：**

```cpp
emplopyeeDao.delete(
        new EntityWrapper<Employee>()
        .eq("last_name","tom")
        .eq("age",16)
);

```

**注：**该案例表示把last_name为tom、age为16的所有用户删除。



总结：

以上便是mybatis-plus的入门教程，介绍了其如何与spring整合、通用crud的使用、全局策略的配置以及条件构造器的使用，但是这并不是MP的所有内容，其强大不限于此。避免篇幅过长，想了解mybatis-plus的更多用法请参考《[mybatis-plus的使用 ------ 进阶](https://www.jianshu.com/p/a4d5d310daf8)》，同时在文末会给出案例的源码。



# 6.lombok

idea中插件lombok

这个插件也没安装上!

## 1 Lombok背景介绍

官方介绍如下：

```
Project Lombok makes java a spicier language by adding 'handlers' that know how to build and compile simple, boilerplate-free, not-quite-java code.

```

大致意思是Lombok通过增加一些“处理程序”，可以让java变得简洁、快速。

2 Lombok使用方法

Lombok能以简单的注解形式来简化java代码，提高开发人员的开发效率。例如开发中经常需要写的javabean，都需要花时间去添加相应的getter/setter，也许还要去写构造器、equals等方法，而且需要维护，当属性多时会出现大量的getter/setter方法，这些显得很冗长也没有太多技术含量，一旦修改属性，就容易出现忘记修改对应方法的失误。

Lombok能通过注解的方式，在编译时自动为属性生成构造器、getter/setter、equals、hashcode、toString方法。出现的神奇就是在源码中没有getter和setter方法，但是在编译生成的字节码文件中有getter和setter方法。这样就省去了手动重建这些代码的麻烦，使代码看起来更简洁些。

Lombok的使用跟引用jar包一样，可以在官网（https://projectlombok.org/download）下载jar包，也可以使用maven添加依赖：

```
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.20</version>
    <scope>provided</scope>
</dependency>

```

接下来我们来分析Lombok中注解的具体用法。

### 2.1 @Data

**这个最牛皮,加了这个注解以后,就不再需要setter和getter方法啦!**

@Data注解在类上，会为类的所有属性自动生成setter/getter、equals、canEqual、hashCode、toString方法，如为final属性，则不会为该属性生成setter方法。

官方实例如下：

[![复制代码](../media/pictures/Microservice.assets/copycode.gif)](javascript:void(0);)

```
 import lombok.AccessLevel;
import lombok.Setter;
import lombok.Data;
import lombok.ToString;

@Data
public class DataExample {
  private final String name;
  @Setter(AccessLevel.PACKAGE) private int age;
  private double score;
  private String[] tags;
  
  @ToString(includeFieldNames=true)
  @Data(staticConstructor="of")
  public static class Exercise<T> {
    private final String name;
    private final T value;
  }
}

```

[![复制代码](../media/pictures/Microservice.assets/copycode.gif)](javascript:void(0);)

如不使用Lombok，则实现如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 import java.util.Arrays;

public class DataExample {
  private final String name;
  private int age;
  private double score;
  private String[] tags;
  
  public DataExample(String name) {
    this.name = name;
  }
  
  public String getName() {
    return this.name;
  }
  
  void setAge(int age) {
    this.age = age;
  }
  
  public int getAge() {
    return this.age;
  }
  
  public void setScore(double score) {
    this.score = score;
  }
  
  public double getScore() {
    return this.score;
  }
  
  public String[] getTags() {
    return this.tags;
  }
  
  public void setTags(String[] tags) {
    this.tags = tags;
  }
  
  @Override public String toString() {
    return "DataExample(" + this.getName() + ", " + this.getAge() + ", " + this.getScore() + ", " + Arrays.deepToString(this.getTags()) + ")";
  }
  
  protected boolean canEqual(Object other) {
    return other instanceof DataExample;
  }
  
  @Override public boolean equals(Object o) {
    if (o == this) return true;
    if (!(o instanceof DataExample)) return false;
    DataExample other = (DataExample) o;
    if (!other.canEqual((Object)this)) return false;
    if (this.getName() == null ? other.getName() != null : !this.getName().equals(other.getName())) return false;
    if (this.getAge() != other.getAge()) return false;
    if (Double.compare(this.getScore(), other.getScore()) != 0) return false;
    if (!Arrays.deepEquals(this.getTags(), other.getTags())) return false;
    return true;
  }
  
  @Override public int hashCode() {
    final int PRIME = 59;
    int result = 1;
    final long temp1 = Double.doubleToLongBits(this.getScore());
    result = (result*PRIME) + (this.getName() == null ? 43 : this.getName().hashCode());
    result = (result*PRIME) + this.getAge();
    result = (result*PRIME) + (int)(temp1 ^ (temp1 >>> 32));
    result = (result*PRIME) + Arrays.deepHashCode(this.getTags());
    return result;
  }
  
  public static class Exercise<T> {
    private final String name;
    private final T value;
    
    private Exercise(String name, T value) {
      this.name = name;
      this.value = value;
    }
    
    public static <T> Exercise<T> of(String name, T value) {
      return new Exercise<T>(name, value);
    }
    
    public String getName() {
      return this.name;
    }
    
    public T getValue() {
      return this.value;
    }
    
    @Override public String toString() {
      return "Exercise(name=" + this.getName() + ", value=" + this.getValue() + ")";
    }
    
    protected boolean canEqual(Object other) {
      return other instanceof Exercise;
    }
    
    @Override public boolean equals(Object o) {
      if (o == this) return true;
      if (!(o instanceof Exercise)) return false;
      Exercise<?> other = (Exercise<?>) o;
      if (!other.canEqual((Object)this)) return false;
      if (this.getName() == null ? other.getValue() != null : !this.getName().equals(other.getName())) return false;
      if (this.getValue() == null ? other.getValue() != null : !this.getValue().equals(other.getValue())) return false;
      return true;
    }
    
    @Override public int hashCode() {
      final int PRIME = 59;
      int result = 1;
      result = (result*PRIME) + (this.getName() == null ? 43 : this.getName().hashCode());
      result = (result*PRIME) + (this.getValue() == null ? 43 : this.getValue().hashCode());
      return result;
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.2 @Getter/@Setter

如果觉得@Data太过残暴（因为@Data集合了@ToString、@EqualsAndHashCode、@Getter/@Setter、@RequiredArgsConstructor的所有特性）不够精细，可以使用@Getter/@Setter注解，此注解在属性上，可以为相应的属性自动生成Getter/Setter方法，示例如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 import lombok.AccessLevel;
import lombok.Getter;
import lombok.Setter;

public class GetterSetterExample {

  @Getter @Setter private int age = 10;
  
  @Setter(AccessLevel.PROTECTED) private String name;
  
  @Override public String toString() {
    return String.format("%s (age: %d)", name, age);
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

如果不使用Lombok：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 public class GetterSetterExample {

  private int age = 10;

  private String name;
  
  @Override public String toString() {
    return String.format("%s (age: %d)", name, age);
  }
  
  public int getAge() {
    return age;
  }
  
  public void setAge(int age) {
    this.age = age;
  }
  
  protected void setName(String name) {
    this.name = name;
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.3 @NonNull

该注解用在属性或构造器上，Lombok会生成一个非空的声明，可用于校验参数，能帮助避免空指针。

示例如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.NonNull;

public class NonNullExample extends Something {
  private String name;
  
  public NonNullExample(@NonNull Person person) {
    super("Hello");
    this.name = person.getName();
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

不使用Lombok：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.NonNull;

public class NonNullExample extends Something {
  private String name;
  
  public NonNullExample(@NonNull Person person) {
    super("Hello");
    if (person == null) {
      throw new NullPointerException("person");
    }
    this.name = person.getName();
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.4 @Cleanup

该注解能帮助我们自动调用close()方法，很大的简化了代码。

示例如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.Cleanup;
import java.io.*;

public class CleanupExample {
  public static void main(String[] args) throws IOException {
    @Cleanup InputStream in = new FileInputStream(args[0]);
    @Cleanup OutputStream out = new FileOutputStream(args[1]);
    byte[] b = new byte[10000];
    while (true) {
      int r = in.read(b);
      if (r == -1) break;
      out.write(b, 0, r);
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

如不使用Lombok，则需如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import java.io.*;

public class CleanupExample {
  public static void main(String[] args) throws IOException {
    InputStream in = new FileInputStream(args[0]);
    try {
      OutputStream out = new FileOutputStream(args[1]);
      try {
        byte[] b = new byte[10000];
        while (true) {
          int r = in.read(b);
          if (r == -1) break;
          out.write(b, 0, r);
        }
      } finally {
        if (out != null) {
          out.close();
        }
      }
    } finally {
      if (in != null) {
        in.close();
      }
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.5 @EqualsAndHashCode

默认情况下，会使用所有非静态（non-static）和非瞬态（non-transient）属性来生成equals和hasCode，也能通过exclude注解来排除一些属性。

示例如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.EqualsAndHashCode;

@EqualsAndHashCode(exclude={"id", "shape"})
public class EqualsAndHashCodeExample {
  private transient int transientVar = 10;
  private String name;
  private double score;
  private Shape shape = new Square(5, 10);
  private String[] tags;
  private int id;
  
  public String getName() {
    return this.name;
  }
  
  @EqualsAndHashCode(callSuper=true)
  public static class Square extends Shape {
    private final int width, height;
    
    public Square(int width, int height) {
      this.width = width;
      this.height = height;
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.6 @ToString

类使用@ToString注解，Lombok会生成一个toString()方法，默认情况下，会输出类名、所有属性（会按照属性定义顺序），用逗号来分割。

通过将`includeFieldNames`参数设为true，就能明确的输出toString()属性。这一点是不是有点绕口，通过代码来看会更清晰些。

使用Lombok的示例：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.ToString;

@ToString(exclude="id")
public class ToStringExample {
  private static final int STATIC_VAR = 10;
  private String name;
  private Shape shape = new Square(5, 10);
  private String[] tags;
  private int id;
  
  public String getName() {
    return this.getName();
  }
  
  @ToString(callSuper=true, includeFieldNames=true)
  public static class Square extends Shape {
    private final int width, height;
    
    public Square(int width, int height) {
      this.width = width;
      this.height = height;
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

不使用Lombok的示例如下：

[![复制代码](D:/Code/Typora/media/pictures/Microservice.assets/copycode.gif)](javascript:void(0);)

```
import java.util.Arrays;

public class ToStringExample {
  private static final int STATIC_VAR = 10;
  private String name;
  private Shape shape = new Square(5, 10);
  private String[] tags;
  private int id;
  
  public String getName() {
    return this.getName();
  }
  
  public static class Square extends Shape {
    private final int width, height;
    
    public Square(int width, int height) {
      this.width = width;
      this.height = height;
    }
    
    @Override public String toString() {
      return "Square(super=" + super.toString() + ", width=" + this.width + ", height=" + this.height + ")";
    }
  }
  
  @Override public String toString() {
    return "ToStringExample(" + this.getName() + ", " + this.shape + ", " + Arrays.deepToString(this.tags) + ")";
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2.7 @NoArgsConstructor, @RequiredArgsConstructor and @AllArgsConstructor

无参构造器、部分参数构造器、全参构造器。Lombok没法实现多种参数构造器的重载。

Lombok示例代码如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import lombok.AccessLevel;
import lombok.RequiredArgsConstructor;
import lombok.AllArgsConstructor;
import lombok.NonNull;

@RequiredArgsConstructor(staticName = "of")
@AllArgsConstructor(access = AccessLevel.PROTECTED)
public class ConstructorExample<T> {
  private int x, y;
  @NonNull private T description;
  
  @NoArgsConstructor
  public static class NoArgsExample {
    @NonNull private String field;
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

不使用Lombok的示例如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 public class ConstructorExample<T> {
  private int x, y;
  @NonNull private T description;
  
  private ConstructorExample(T description) {
    if (description == null) throw new NullPointerException("description");
    this.description = description;
  }
  
  public static <T> ConstructorExample<T> of(T description) {
    return new ConstructorExample<T>(description);
  }
  
  @java.beans.ConstructorProperties({"x", "y", "description"})
  protected ConstructorExample(int x, int y, T description) {
    if (description == null) throw new NullPointerException("description");
    this.x = x;
    this.y = y;
    this.description = description;
  }
  
  public static class NoArgsExample {
    @NonNull private String field;
    
    public NoArgsExample() {
    }
  }
}

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 3 Lombok工作原理分析

会发现在Lombok使用的过程中，只需要添加相应的注解，无需再为此写任何代码。自动生成的代码到底是如何产生的呢？

核心之处就是对于注解的解析上。JDK5引入了注解的同时，也提供了两种解析方式。

- 运行时解析

运行时能够解析的注解，必须将@Retention设置为RUNTIME，这样就可以通过反射拿到该注解。java.lang,reflect反射包中提供了一个接口AnnotatedElement，该接口定义了获取注解信息的几个方法，Class、Constructor、Field、Method、Package等都实现了该接口，对反射熟悉的朋友应该都会很熟悉这种解析方式。

- 编译时解析

编译时解析有两种机制，分别简单描述下：

1）Annotation Processing Tool

apt自JDK5产生，JDK7已标记为过期，不推荐使用，JDK8中已彻底删除，自JDK6开始，可以使用Pluggable Annotation Processing API来替换它，apt被替换主要有2点原因：

- api都在com.sun.mirror非标准包下
- 没有集成到javac中，需要额外运行

2）Pluggable Annotation Processing API

[JSR 269](https://jcp.org/en/jsr/detail?id=269)自JDK6加入，作为apt的替代方案，它解决了apt的两个问题，javac在执行的时候会调用实现了该API的程序，这样我们就可以对编译器做一些增强，这时javac执行的过程如下：
![这里写图片描述](D:/Code/Typora/media/pictures/Microservice.assets/20160908130644281)

Lombok本质上就是一个实现了“[JSR 269 API](https://www.jcp.org/en/jsr/detail?id=269)”的程序。在使用javac的过程中，它产生作用的具体流程如下：

1. javac对源代码进行分析，生成了一棵抽象语法树（AST）
2. 运行过程中调用实现了“JSR 269 API”的Lombok程序
3. 此时Lombok就对第一步骤得到的AST进行处理，找到@Data注解所在类对应的语法树（AST），然后修改该语法树（AST），增加getter和setter方法定义的相应树节点
4. javac使用修改后的抽象语法树（AST）生成字节码文件，即给class增加新的节点（代码块）

拜读了Lombok源码，对应注解的实现都在HandleXXX中，比如@Getter注解的实现时HandleGetter.handle()。还有一些其它类库使用这种方式实现，比如[Google Auto](https://github.com/google/auto)、[Dagger](http://square.github.io/dagger/)等等。

## 4. Lombok的优缺点

优点：

1. 能通过注解的形式自动生成构造器、getter/setter、equals、hashcode、toString等方法，提高了一定的开发效率
2. 让代码变得简洁，不用过多的去关注相应的方法
3. 属性做修改时，也简化了维护为这些属性所生成的getter/setter方法等

缺点：

1. 不支持多种参数构造器的重载
2. 虽然省去了手动创建getter/setter方法的麻烦，但大大降低了源代码的可读性和完整性，降低了阅读源代码的舒适度

## 5. 总结

Lombok虽然有很多优点，但Lombok更类似于一种IDE插件，项目也需要依赖相应的jar包。Lombok依赖jar包是因为编译时要用它的注解，为什么说它又类似插件？因为在使用时，eclipse或IntelliJ IDEA都需要安装相应的插件，在编译器编译时通过操作AST（抽象语法树）改变字节码生成，变向的就是说它在改变java语法。它不像spring的依赖注入或者mybatis的ORM一样是运行时的特性，而是编译时的特性。这里我个人最感觉不爽的地方就是对插件的依赖！因为Lombok只是省去了一些人工生成代码的麻烦，但IDE都有快捷键来协助生成getter/setter等方法，也非常方便。

知乎上有位大神发表过对Lombok的一些看法：

```
这是一种低级趣味的插件，不建议使用。JAVA发展到今天，各种插件层出不穷，如何甄别各种插件的优劣？能从架构上优化你的设计的，能提高应用程序性能的 ，实现高度封装可扩展的...， 像lombok这种，像这种插件，已经不仅仅是插件了，改变了你如何编写源码，事实上，少去了代码你写上去又如何？ 如果JAVA家族到处充斥这样的东西，那只不过是一坨披着金属颜色的屎，迟早会被其它的语言取代。

```

虽然话糙但理确实不糙，试想一个项目有非常多类似Lombok这样的插件，个人觉得真的会极大的降低阅读源代码的舒适度。

虽然非常不建议在属性的getter/setter写一些业务代码，但在多年项目的实战中，有时通过给getter/setter加一点点业务代码，能极大的简化某些业务场景的代码。所谓取舍，也许就是这时的舍弃一定的规范，取得极大的方便。

我现在非常坚信一条理念，任何编程语言或插件，都仅仅只是工具而已，即使工具再强大也在于用的人，就如同小米加步枪照样能赢飞机大炮的道理一样。结合具体业务场景和项目实际情况，无需一味追求高大上的技术，适合的才是王道。

Lombok有它的得天独厚的优点，也有它避之不及的缺点，熟知其优缺点，在实战中灵活运用才是王道。



就是bean上面加东西的!看10.14记录!

## @Resource注解

**@Resource和@Autowired注解都是用来实现依赖注入的。**只是@AutoWried按by type自动注入，而@Resource默认按byName自动注入。

@Resource有两个重要属性，分别是name和type

spring将name属性解析为bean的名字，而type属性则被解析为bean的类型。所以如果使用name属性，则使用byName的自动注入策略，如果使用type属性则使用byType的自动注入策略。如果都没有指定，则通过反射机制使用byName自动注入策略。

@Resource依赖注入时查找bean的规则：(以用在field上为例)

既不指定name属性，也不指定type属性，则自动按byName方式进行查找。如果没有找到符合的bean，则回退为一个原始类型进行查找，如果找到就注入。

此时name是变量名.



# 7.redis

## redis介绍

Nosql 非关系型数据库

百科

Redis

可基于内存 , 可持久化的日志型、Key-Value数据库

去取数据的时候，指定key即可。不能用sql语句。

Redis是一个开源的内存数据库，它以键值对的形式存储数据。由于数据存储在内存中，因此Redis的速度很快，但是每次重启Redis服务时，其中的数据也可能会丢失，因此，Redis也提供了持久化存储机制，将数据以某种形式保存在文件中，每次重启时，可以自动从文件加载数据到内存当中.

### Windows 

绿色版 （建议使用）

![](../media/pictures/Microservice.assets/26987014e8aa6aad9ea36d4078a49351.png)

安装版

![](../media/pictures/Microservice.assets/b83749ed102ddda6ad3aebba339c844e.png)

建议redis安装的目录增加到环境变量。

D:\\Program Files\\redis

### Linux

![](../media/pictures/Microservice.assets/9617b1815c3f65e73873813320cd7d5e.png)

![](../media/pictures/Microservice.assets/42e5f5b68cf0f8390addeb847a4e51f4.png)

启动

![](../media/pictures/Microservice.assets/d1d4a272ce44274df0b32647fb6ede9c.png)

![](../media/pictures/Microservice.assets/95de5705fb9ade0dd4eb02172e5fe75f.png)

![](../media/pictures/Microservice.assets/56e8ad6e30e5c84fa73450fab7575adc.png)

启动

![](../media/pictures/Microservice.assets/93323a663c2d99f6a47d1728ac10c6d9.png)

![](../media/pictures/Microservice.assets/4da5030227ee1323cdfeb6f3c051beaa.png)

![](../media/pictures/Microservice.assets/e30235c417d952b374c6277c6deaae5d.png)

![](../media/pictures/Microservice.assets/7cb792141f451881b9cf813c978bcefb.png)

## 启动

**首先要启动服务器,然后才可以启动客户端!**

redis-server 6379 服务器

redis-cli 客户端 

## 配置介绍

## redis.conf

### bind

![](../media/pictures/Microservice.assets/c3d2f9175e503389fdb64699ed85fcda.png)

外网使用不了

改成0.0.0.0

### 端口号

![](../media/pictures/Microservice.assets/437d081b778c7b8b2d796df65873aad5.png)

通常不需要修改

### 保存时间

![](../media/pictures/Microservice.assets/9f32d3fe685e043f9a56e51b13da0659.png)

![1571148546862](../media/pictures/Microservice.assets/1571148546862.png)

上面这个三个,每一次只能启动其中一个,三个之间没有包含关系!

上面的save 900 1意思是,900秒,如果有一次修改,时间和次数同时满足才会触发!

下面的save 60 10000 是60秒,修改10000次,才会修改!

触发最下面的一个的时候,是不会触发上面的一个的!



### 存储策略

#### RDB

Redis DataBase

Redis 默认的存储策略

![](../media/pictures/Microservice.assets/eec51808b545d413e636f8ef936dd870.png)

#### AOF

Append-only file

保存策略

## 基本使用

### 命令行下使用

### Demo

Redis 是key value形式的存储系统（nosql数据库）

我们所有存的东西，都需要有个key

Redis Vs HashMap

只是我们之前value 可以存很多对象，

Redis里value 默认支持常见的数据结构。

HashMap\<String ,Object\> 可以put任何对象。

而redis通过key去保存的值，只能是特定的一些结构。

操作不同的数据结构的时候，redis提供了不同的命令。

#### 字符串（value的类型）

跟之前的map 非常类似。Value是字符串。

- [SET](http://doc.redisfans.com/string/set.html) key value
- [GET](http://doc.redisfans.com/string/get.html) key
- [INCR](http://doc.redisfans.com/string/incr.html)
  可以对应的key的数值（整型的数值）加一
- [INCRBY](http://doc.redisfans.com/string/incrby.html) 给数值加上一个步长
- [SETEX](http://doc.redisfans.com/string/setex.html) expire 过期
- [SETNX](http://doc.redisfans.com/string/setnx.html) not exist
  key不存在的时候再去赋值

#### LIST

- [LPUSH](http://doc.redisfans.com/list/lpush.html)

![](../media/pictures/Microservice.assets/d5f125450d82fcd83772785dd48feffd.png)

> 后面的元素放在栈顶 （）

- [LPOP](http://doc.redisfans.com/list/lpop.html)

> 返回第一个元素，并且在列表上删除该元素 （栈顶）

- [LLEN](http://doc.redisfans.com/list/llen.html)

> 返回当前的list列表的长度

![](../media/pictures/Microservice.assets/52b904a6e7937cf1204005084fc26ced.png)

- [LINDEX](http://doc.redisfans.com/list/lindex.html)

> 返回当前的list的指定index下标的元素。没有返回nil

> 0表示栈顶的元素

![](../media/pictures/Microservice.assets/bbc21bac6f4184feae4c5d74685f9f72.png)

- [LINSERT](http://doc.redisfans.com/list/linsert.html)

> 插入的位置是按照index的顺序

> Before的话得注意 index的值

![](../media/pictures/Microservice.assets/a26789bac0ff2b978135f65d13212994.png)

![](../media/pictures/Microservice.assets/a91e57dbd0df5e9a70a34bfd20beb017.png)

- [LPUSHX](http://doc.redisfans.com/list/lpushx.html)

> 如果list存在，再去push

![](../media/pictures/Microservice.assets/a3978e45ecde37a97a0d6355741e53ba.png)

- [LRANGE](http://doc.redisfans.com/list/lrange.html)

> 可以方便的查看某个index范围内的lislt的值

> 输入的index是从0开始，显示的标号是从1开始的。

![](../media/pictures/Microservice.assets/8b21d03c29ad8490a7af14e1828d6a4d.png)

- [LREM](http://doc.redisfans.com/list/lrem.html)

> 删除list里的指定的前几个（指定value的）元素

> 比如 lrem my12list 2 123 意思是删除前两个 123

![](../media/pictures/Microservice.assets/45902f412ef1d245c4129a7e709719b1.png)

![](../media/pictures/Microservice.assets/e3018c2f26290640fe76acc2394067ed.png)

> Value表示删除的元素

> Count表示删除几个该元素 从列表的第一个开始找

> 删除指定位置的元素：没有

- [LSET](http://doc.redisfans.com/list/lset.html)
- 设置指定的位置的元素的值 （修改）
- 输入的index是从0开始，显示的标号是从1开始的。

![](../media/pictures/Microservice.assets/d51eb4d471e05f5d37c0b3a8ca96eef1.png)

#### Hash （二维表）

User{

> Username:zhangsan  
> age :18

> Email:zs\@163.colm

}

值哈希表 key value

- [HSET](http://doc.redisfans.com/hash/hset.html)

![](../media/pictures/Microservice.assets/c49c565e81f7c6c2402a8ab8be29c0fd.png)

- [HGET](http://doc.redisfans.com/hash/hget.html)

> 给一个hash表的key，返回一个值

![](../media/pictures/Microservice.assets/46ed9d080eb023784deb58683ee53139.png)

- [HEXISTS](http://doc.redisfans.com/hash/hexists.html)

> 表里的key是否存在

![](../media/pictures/Microservice.assets/df37dd793998b828f0df0443541f4261.png)

- [HGETALL](http://doc.redisfans.com/hash/hgetall.html)

> 返回hash表里的所有元素

![](../media/pictures/Microservice.assets/0433919d2e610cedace2bb03844dcd7b.png)

- [HKEYS](http://doc.redisfans.com/hash/hkeys.html)

![](../media/pictures/Microservice.assets/27ce992fe3f1c310f39b322969d5006e.png)

- [HLEN](http://doc.redisfans.com/hash/hlen.html)

> 有几个元素（几行数据）

![](../media/pictures/Microservice.assets/955b74186405b060caca3a2399907a75.png)

- [HVALS](http://doc.redisfans.com/hash/hvals.html)

![](../media/pictures/Microservice.assets/eb180d767000ab630056aa5c574e1efd.png)

- [HINCRBY](http://doc.redisfans.com/hash/hincrby.html)

![](../media/pictures/Microservice.assets/1a871268bed1733e6ad49660b9d95389.png)

- [HMGET](http://doc.redisfans.com/hash/hmget.html)

> Many

> 给一个hash表的多个key，返回多个值

![](../media/pictures/Microservice.assets/5214fd1fc33d39851085c14c25090c08.png)

- [HMSET](http://doc.redisfans.com/hash/hmset.html)

![](../media/pictures/Microservice.assets/043eab9ce270112ad241da6aa2ca83af.png)

- [HSETNX](http://doc.redisfans.com/hash/hsetnx.html)

> Not exist 不存在会创建一个key，然后设置值

![](../media/pictures/Microservice.assets/49e9461cc2cb913dfc0e118b8c8d74ed.png)

> 存在，不改变该key 的值

![](../media/pictures/Microservice.assets/4cf2317987566f3692d522356563b16d.png)

#### Set（无序集合）

- [SADD](http://doc.redisfans.com/set/sadd.html)

> 往set集合里增加一个或者多个元素

![](../media/pictures/Microservice.assets/f4a7e83f078d5a9c6fa9e7f3c71a14d4.png)

- [SMEMBERS](http://doc.redisfans.com/set/smembers.html)

> 列出这个集合里的所有元素

![](../media/pictures/Microservice.assets/b2a5f9ecb36dc179166d7dcf5688ab83.png)

- [SISMEMBER](http://doc.redisfans.com/set/sismember.html)

> 是否存在在当前的集合中

![](../media/pictures/Microservice.assets/dbf65d4f2ef9f8284b80da5879118810.png)

- [SCARD](http://doc.redisfans.com/set/scard.html)

> 集合的长度

![](../media/pictures/Microservice.assets/13493b95096a0417e34a498279af2d03.png)

- [SPOP](http://doc.redisfans.com/set/spop.html) （弹出并从集合删除）

> 取出集合里的5个元素

![](../media/pictures/Microservice.assets/11664da1f7d73648aad717f7b91a1489.png)

- [SRANDMEMBER](http://doc.redisfans.com/set/srandmember.html)

> 随机取出 5个元素（不删除）

![](../media/pictures/Microservice.assets/cb16f247eeca5079c66bf6863a06869a.png)

- [SINTER](http://doc.redisfans.com/set/sinter.html)

> 求出两个集合的相交部分

![](../media/pictures/Microservice.assets/0c0de43df363e67a25d1bcac10bd30fd.png)

- [SINTERSTORE](http://doc.redisfans.com/set/sinterstore.html)

> 把相交的集合保存起来

- [SUNION](http://doc.redisfans.com/set/sunion.html)

> 求两个集合的并集

![](../media/pictures/Microservice.assets/9493d809927a6896bcb295e65bc66d5d.png)

- [SUNIONSTORE](http://doc.redisfans.com/set/sunionstore.html)
- [SDIFF](http://doc.redisfans.com/set/sdiff.html)

> 参数1 减去参数1和2的交集

![](../media/pictures/Microservice.assets/7c20513f4b02c8b6882afb4e35aacf6f.png)

- [SDIFFSTORE](http://doc.redisfans.com/set/sdiffstore.html)

> 同上，SDIFFSTORE destination key1 [key2] 返回给定所有集合的差集并存储在
> destination 中

- [SMOVE](http://doc.redisfans.com/set/smove.html)

![](../media/pictures/Microservice.assets/22445ccb3454652ecf3214d5ff387d53.png)

- [SREM](http://doc.redisfans.com/set/srem.html) 删除

![](../media/pictures/Microservice.assets/2146fc2c27fd75c6335bb4109a87fe5c.png)

> 你的关注的人

> 他关注的人

> 的共同部分 sinter 就是共同关注的

#### SortSet

有序的集合，它是可以给一个值 赋予一个分值，根据分值来排序

- [ZADD](http://doc.redisfans.com/sorted_set/zadd.html)

![](../media/pictures/Microservice.assets/6037cd01e3f1d35606a7f201c31c31b1.png)

- [ZCARD](http://doc.redisfans.com/sorted_set/zcard.html)

> 长度

![](../media/pictures/Microservice.assets/94c87bdbf2b2c6821e425bf34da3a1ad.png)

- [ZSCORE](http://doc.redisfans.com/sorted_set/zscore.html)

![](../media/pictures/Microservice.assets/da34c4f3380a7ef61bdc689dba56c7b6.png)

- [ZCOUNT](http://doc.redisfans.com/sorted_set/zcount.html) （闭区间）

![](../media/pictures/Microservice.assets/9b0af64edadf6f06ef53ea4f5a3ffa25.png)

- [ZINCRBY](http://doc.redisfans.com/sorted_set/zincrby.html)

![](../media/pictures/Microservice.assets/4c469f20b3f3b44a0a2d5569d70cdd8b.png)

- [ZRANGE](http://doc.redisfans.com/sorted_set/zrange.html)

> 根据排名给出范围

![](../media/pictures/Microservice.assets/3e0e81409cc995f243a345c3a1867859.png)

- [ZRANGEBYSCORE](http://doc.redisfans.com/sorted_set/zrangebyscore.html)

> 根据指定的分值范围去查找

![](../media/pictures/Microservice.assets/96ca656c1ebbbc5ef150669afa176964.png)

- [ZRANK](http://doc.redisfans.com/sorted_set/zrank.html) （排名从0开始）

![](../media/pictures/Microservice.assets/abdcf2314af087b7c1f5df360d596cef.png)

- [ZREVRANGE](http://doc.redisfans.com/sorted_set/zrevrange.html)
- 先全部反转，在去对应的index的value

![](../media/pictures/Microservice.assets/291f76107d0cc8bef593e4c3ac28fab4.png)

- [ZREVRANGEBYSCORE](http://doc.redisfans.com/sorted_set/zrevrangebyscore.html)

![](../media/pictures/Microservice.assets/0ab9f6e487d84d3478b3a3129dd954ba.png)

- [ZREVRANK](http://doc.redisfans.com/sorted_set/zrevrank.html)

> 返回一个逆序的排名值

![](../media/pictures/Microservice.assets/7d2c77cbe7fc17daefd5e91f053b8b4a.png)

- [ZREM](http://doc.redisfans.com/sorted_set/zrem.html)

> 删除

- [ZREMRANGEBYRANK](http://doc.redisfans.com/sorted_set/zremrangebyrank.html)

> 删除指定排名的成员

![](../media/pictures/Microservice.assets/d9b125c88935c9dea16790ce6cfe1259.png)

- [ZREMRANGEBYSCORE](http://doc.redisfans.com/sorted_set/zremrangebyscore.html)

> 删除指定分数区间的成员

![](../media/pictures/Microservice.assets/f401fb48e41895adbe57f1784bca3082.png)

### 代码里使用

1 jedis

增加依赖

![](../media/pictures/Microservice.assets/d7f75220ccdd907536c4dd23ac4c59d2.png)

2 RedisTemplate

导包 导的是spring boot对redis的支持包

```xml
<!-- redis RedisTemplate 经过测试 这个是可以用的!-->
<!--StringRedisTemplate--> 
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

```

\<**dependency**\>  
\<**groupId**\>org.springframework.boot\</**groupId**\>  
\<**artifactId**\>spring-boot-starter-data-redis\</**artifactId**\>  
\</**dependency**\>

设置序列化

![](../media/pictures/Microservice.assets/eb2fa28dc6582e4e66979baba2895499.png)

#### 基本使用

![](../media/pictures/Microservice.assets/7b3b56ec155a0a925824b44add2e5598.png)

#### 优化一下

## 项目实战

点赞点踩

用哪种数据结构实现

Set

Key ： newsid_like

集合里放的是什么？ { 1 }

newsid_dislike {

}

## redis单点登录

1 单点登陆流程图

下图和我们使用单点登陆原理一致，只是我们项目中是在生成token之后直接返回给前端，图中是放在cookie中返回给前端

![](../media/pictures/Microservice.assets/d7fe5837dd16d606342a84502471a08f.png)

参考链接：*https://blog.csdn.net/qq_22172133/article/details/82291112*

导包：

![](../media/pictures/Microservice.assets/4abb12febb20ef34b361553db810b26d.png)

```xml
<!--redis 单点登录-->
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
</dependency>

```

2，我们需要在Guns-Gateway里面去做鉴权，那么需要我们的网关项目接入redis

3，我们jedis的客户端是相当于和redis服务之间新建一个连接，我们程序运行的时候不可能在我们每次需要用到redis的时候就去建立连接，所以我们需要在spring容器里面维护一个Jedis对象，或者是RedisTemplate对象，如下

![](../media/pictures/Microservice.assets/79053f72aedfc9cf044f5ae7f350c392.png)

然后通过下面这种方式来引入jedis

![](../media/pictures/Microservice.assets/56b62e4680893f51784b0ad5746dadf1.png)

然后实现单点登陆，把我注释的部分补充完整即可

步骤1： 把token 和 userId 作为key-value存入redis 中

![](../media/pictures/Microservice.assets/cac2fc0b73bbc2a406cc9c6e8eee2c26.png)

步骤2：
后端把token存入缓存之后，那么下次请求过来，在经过**AuthFilter**的时候，我们获取到了前端发送过来的token，之后我们可以通过这个token去redis
里面取userId，如果没去到，说明redis里面的数据已经过期

![](../media/pictures/Microservice.assets/52a67f67934144120637e65c4bb39a6d.png)

## Jedis和RedisTemplate有何区别？

Jedis是Redis官方推荐的面向Java的操作Redis的客户端，而RedisTemplate是SpringDataRedis中对JedisApi的高度封装。
SpringDataRedis相对于Jedis来说可以方便地更换Redis的Java客户端，比Jedis多了自动管理连接池的特性，方便与其他Spring框架进行搭配使用如：SpringCache

![1571833084560](../media/pictures/Microservice.assets/1571833084560.png)

他们两个执行速率不一样!  

jedis比较原生,速度快!

RedisTemplate是Spring分装的,功能强大,但是速度慢!



# 8.订单支付

支付宝订单支付 

支付宝沙箱 需要登录上 才可以下载!

project3书签中,可以找到的!



详细看老师ailipaydemo中!



# 9.整合nginx



整合nginx要启动nginx,还要解决跨域问



# 10.数据库SQL优化

这个视频是在bilibili上面找的https://www.bilibili.com/video/av29072634/?p=5!讲的还行!笔记在github上面,星里面!下载下来的笔记在总结里面!

## (1).MySQL版本：

5.x:
5.0-5.1:早期产品的延续，升级维护
5.4 - 5.x :  MySQL整合了三方公司的新存储引擎 （推荐5.5）
	

安装：rpm -ivh rpm软件名
	如果安装时 与某个软件  xxx冲突，则需要将冲突的软件卸载掉：
		yun -y remove xxx
	安装时 有日志提示我们可以修改密码：/usr/bin/mysqladmin -u root password 'new-password'

注意： 
		如果提示“GPG keys...”安装失败，解决方案：
		rpm -ivh rpm软件名  --force --nodoeps
	
验证：
mysqladmin --version

启动mysql应用： service mysql start
关闭： service mysql stop
重启： service mysql restart

在计算机reboot后 登陆MySQL :  mysql
可能会报错：   "/var/lib/mysql/mysql.sock不存在"  
--原因：是Mysql服务没有启动
解决 ：  启动服务： 1.每次使用前 手动启动服务   /etc/init.d/mysql start
	  	 2.开机自启   chkconfig mysql on     ,  chkconfig mysql off    
	检查开机是否自动启动： ntsysv		
	
给mysql 的超级管理员root 增加密码：/usr/bin/mysqladmin -u root password root
				
登陆：
mysql -u root -p

数据库存放目录：
ps -ef|grep mysql  可以看到：
	数据库目录：     datadir=/var/lib/mysql 
	pid文件目录： --pid-file=/var/lib/mysql/bigdata01.pid

​	MySQL核心目录：
​		/var/lib/mysql :mysql 安装目录
​		/usr/share/mysql:  配置文件
​		/usr/bin：命令目录（mysqladmin、mysqldump等）
​		/etc/init.d/mysql启停脚本
​		
  MySQL配置文件
​		 my-huge.cnf	高端服务器  1-2G内存
​		 my-large.cnf   中等规模
​		 my-medium.cnf  一般
​		 my-small.cnf   较小
​		但是，以上配置文件mysql默认不能识别，默认只能识别 /etc/my.cnf
​		采用 my-huge.cnf ：
​		cp /usr/share/mysql/my-huge.cnf /etc/my.cnf
​		注意：mysql5.5默认配置文件/etc/my.cnf；Mysql5.6 默认配置文件/etc/mysql-default.cnf
​		
默认端口3306
mysql字符编码：
​	sql  :  show variables like '%char%' ;
​	可以发现部分编码是 latin,需要统一设置为utf-8
​	设置编码：
​	vi /etc/my.cnf:
​	[mysql]
​	default-character-set=utf8
​	[client]
​	default-character-set=utf8
​	
​	[mysqld]
​	character_set_server=utf8
​	character_set_client=utf8
​	collation_server=utf8_general_ci

重启Mysql:  service mysql restart
	sql  :  show variables like '%char%' ;
注意事项：修改编码 只对“之后”创建的数据库生效，因此 我们建议 在mysql安装完毕后，第一时间 统一编码。

mysql:清屏    ctrl+L    , system clear

## (2).原理

  MYSQL逻辑分层 ：连接层 服务层 引擎层 存储层

​	  InnoDB(默认) ：事务优先 （适合高并发操作；行锁）
 	 MyISAM ：性能优先  （表锁）

查询数据库引擎：  支持哪些引擎？ show engines ;
		查看当前使用的引擎   show variables like '%storage_engine%' ;

指定数据库对象的引擎：
create table tb(
		id int(4) auto_increment ,
		name varchar(5),
		dept varchar(5) ,
		primary key(id)		
)ENGINE=MyISAM AUTO_INCREMENT=1
 DEFAULT CHARSET=utf8   ;

## (3).SQL优化

​	原因：性能低、执行时间太长、等待时间太长、SQL语句欠佳（连接查询）、索引失效、服务器参数设置不合理（缓冲、线程数）



**SQL编写过程和执行过程不一样!**

**a.SQL ：**
	编写过程：(sinstinct去重!)
		select dinstinct  ..from  ..join ..on ..where ..group by ...having ..order by ..limit ..

​	解析过程：			
​		from .. on.. join ..where ..group by ....having ...select dinstinct ..order by limit ...



**b.SQL优化， 主要就是 在优化索引**
	索引： 相当于书的目录
	索引： index是帮助MYSQL高效获取数据的数据结构。索引是数据结构（树：B树(默认)、Hash树...）

​	索引的**弊端**：
​		1.**索引本身很大**， 可以存放在内存/硬盘（通常为 硬盘）
​		2.索引不是所有情况均适用： a.少量数据  b.频繁更新的字段   c.很少使用的字段
​		3.索引会降低增删改的效率（增删改  查）

​	**优势**：1提高查询效率（降低IO使用率）
​	      2.降低CPU使用率 （...order by age desc,因为 B树索引 本身就是一个 好排序的结构，因此在排序时  可以直接使用）

**这里要用到数据结构的B树!**

假如第一个为索引的第一个节点!

B树:

![1571314740799](../media/pictures/Microservice.assets/1571314740799.png)

B树索引原理:

![1571316935576](../media/pictures/Microservice.assets/1571316935576.png)

### **SQL解析顺序:**

这里是原文链接!https://www.cnblogs.com/annsshadow/p/5037667.html

　　一直是想知道一条SQL语句是怎么被执行的，它执行的顺序是怎样的，然后查看总结各方资料，就有了下面这一篇博文了。

　　本文将从MySQL总体架构--->查询执行流程--->语句执行顺序来探讨一下其中的知识。



#### **一、MySQL架构总览：**

　　架构最好看图，再配上必要的说明文字。

　　下图根据参考书籍中一图为原本，再在其上添加上了自己的理解。

![img](https://images2015.cnblogs.com/blog/701942/201512/701942-20151210224128402-1287669438.png)

 

　　从上图中我们可以看到，整个架构分为两层，上层是MySQLD的被称为的‘SQL Layer’，下层是各种各样对上提供接口的存储引擎，被称为‘Storage Engine Layer’。其它各个模块和组件，从名字上就可以简单了解到它们的作用，这里就不再累述了。

 

#### **二、查询执行流程**

　　下面再向前走一些，容我根据自己的认识说一下查询执行的流程是怎样的：

**1.连接**

　　1.1客户端发起一条Query请求，监听客户端的‘连接管理模块’接收请求

　　1.2将请求转发到‘连接进/线程模块’

　　1.3调用‘用户模块’来进行授权检查

　　1.4通过检查后，‘连接进/线程模块’从‘线程连接池’中取出空闲的被缓存的连接线程和客户端请求对接，如果失败则创建一个新的连接请求

 

**2.处理**

　　2.1先查询缓存，检查Query语句是否完全匹配，接着再检查是否具有权限，都成功则直接取数据返回

　　2.2上一步有失败则转交给‘命令解析器’，经过词法分析，语法分析后生成解析树

　　2.3接下来是预处理阶段，处理解析器无法解决的语义，检查权限等，生成新的解析树

　　2.4再转交给对应的模块处理

　　2.5如果是SELECT查询还会经由‘查询优化器’做大量的优化，生成执行计划

　　2.6模块收到请求后，通过‘访问控制模块’检查所连接的用户是否有访问目标表和目标字段的权限

　　2.7有则调用‘表管理模块’，先是查看table cache中是否存在，有则直接对应的表和获取锁，否则重新打开表文件

　　2.8根据表的meta数据，获取表的存储引擎类型等信息，通过接口调用对应的存储引擎处理

　　2.9上述过程中产生数据变化的时候，若打开日志功能，则会记录到相应二进制日志文件中

 

**3.结果**

　　3.1Query请求完成后，将结果集返回给‘连接进/线程模块’

　　3.2返回的也可以是相应的状态标识，如成功或失败等

　　3.3‘连接进/线程模块’进行后续的清理工作，并继续等待请求或断开与客户端的连接

 

**一图小总结**

**![img](https://images2015.cnblogs.com/blog/701942/201512/701942-20151210224221011-1559007674.png)**

 

 

**三、SQL解析顺序**

　　接下来再走一步，让我们看看一条SQL语句的前世今生。

　　首先看一下示例语句

[![复制代码](../media/pictures/Microservice.assets/copycode-1571313428425.gif)](javascript:void(0);)

```
SELECT DISTINCT
    < select_list >
FROM
    < left_table > < join_type >
JOIN < right_table > ON < join_condition >
WHERE
    < where_condition >
GROUP BY
    < group_by_list >
HAVING
    < having_condition >
ORDER BY
    < order_by_condition >
LIMIT < limit_number >

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　然而它的执行顺序是这样的

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 FROM <left_table>
 2 ON <join_condition>
 3 <join_type> JOIN <right_table>
 4 WHERE <where_condition>
 5 GROUP BY <group_by_list>
 6 HAVING <having_condition>
 7 SELECT 
 8 DISTINCT <select_list>
 9 ORDER BY <order_by_condition>
10 LIMIT <limit_number>

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　虽然自己没想到是这样的，不过一看还是很自然和谐的，从哪里获取，不断的过滤条件，要选择一样或不一样的，排好序，那才知道要取前几条呢。

既然如此了，那就让我们一步步来看看其中的细节吧。

 

**准备工作**

　　1.创建测试数据库

```
create database testQuery

```

　　2.创建测试表

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
CREATE TABLE table1
(
    uid VARCHAR(10) NOT NULL,
    name VARCHAR(10) NOT NULL,
    PRIMARY KEY(uid)
)ENGINE=INNODB DEFAULT CHARSET=UTF8;

CREATE TABLE table2
(
    oid INT NOT NULL auto_increment,
    uid VARCHAR(10),
    PRIMARY KEY(oid)
)ENGINE=INNODB DEFAULT CHARSET=UTF8;

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　3.插入数据

```
INSERT INTO table1(uid,name) VALUES('aaa','mike'),('bbb','jack'),('ccc','mike'),('ddd','mike');

INSERT INTO table2(uid) VALUES('aaa'),('aaa'),('bbb'),('bbb'),('bbb'),('ccc'),(NULL);

```

　　4.最后想要的结果

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
SELECT
    a.uid,
    count(b.oid) AS total
FROM
    table1 AS a
LEFT JOIN table2 AS b ON a.uid = b.uid
WHERE
    a. NAME = 'mike'
GROUP BY
    a.uid
HAVING
    count(b.oid) < 2
ORDER BY
    total DESC
LIMIT 1;

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

！现在开始SQL解析之旅吧！

 

**1. FROM**

当涉及多个表的时候，左边表的输出会作为右边表的输入，之后会生成一个虚拟表VT1。

(1-J1)笛卡尔积

计算两个相关联表的笛卡尔积(CROSS JOIN) ，生成虚拟表VT1-J1。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> select * from table1,table2;
+-----+------+-----+------+
| uid | name | oid | uid  |
+-----+------+-----+------+
| aaa | mike |   1 | aaa  |
| bbb | jack |   1 | aaa  |
| ccc | mike |   1 | aaa  |
| ddd | mike |   1 | aaa  |
| aaa | mike |   2 | aaa  |
| bbb | jack |   2 | aaa  |
| ccc | mike |   2 | aaa  |
| ddd | mike |   2 | aaa  |
| aaa | mike |   3 | bbb  |
| bbb | jack |   3 | bbb  |
| ccc | mike |   3 | bbb  |
| ddd | mike |   3 | bbb  |
| aaa | mike |   4 | bbb  |
| bbb | jack |   4 | bbb  |
| ccc | mike |   4 | bbb  |
| ddd | mike |   4 | bbb  |
| aaa | mike |   5 | bbb  |
| bbb | jack |   5 | bbb  |
| ccc | mike |   5 | bbb  |
| ddd | mike |   5 | bbb  |
| aaa | mike |   6 | ccc  |
| bbb | jack |   6 | ccc  |
| ccc | mike |   6 | ccc  |
| ddd | mike |   6 | ccc  |
| aaa | mike |   7 | NULL |
| bbb | jack |   7 | NULL |
| ccc | mike |   7 | NULL |
| ddd | mike |   7 | NULL |
+-----+------+-----+------+
28 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

(1-J2)ON过滤

基于虚拟表VT1-J1这一个虚拟表进行过滤，过滤出所有满足ON 谓词条件的列，生成虚拟表VT1-J2。

注意：这里因为语法限制，使用了'WHERE'代替，从中读者也可以感受到两者之间微妙的关系；

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> *
    -> FROM
    -> table1,
    -> table2
    -> WHERE
    -> table1.uid = table2.uid
    -> ;
+-----+------+-----+------+
| uid | name | oid | uid  |
+-----+------+-----+------+
| aaa | mike |   1 | aaa  |
| aaa | mike |   2 | aaa  |
| bbb | jack |   3 | bbb  |
| bbb | jack |   4 | bbb  |
| bbb | jack |   5 | bbb  |
| ccc | mike |   6 | ccc  |
+-----+------+-----+------+
6 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

(1-J3)添加外部列

如果使用了外连接(LEFT,RIGHT,FULL)，主表（保留表）中的不符合ON条件的列也会被加入到VT1-J2中，作为外部行，生成虚拟表VT1-J3。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> *
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid;
+-----+------+------+------+
| uid | name | oid  | uid  |
+-----+------+------+------+
| aaa | mike |    1 | aaa  |
| aaa | mike |    2 | aaa  |
| bbb | jack |    3 | bbb  |
| bbb | jack |    4 | bbb  |
| bbb | jack |    5 | bbb  |
| ccc | mike |    6 | ccc  |
| ddd | mike | NULL | NULL |
+-----+------+------+------+
7 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

下面从网上找到一张很形象的关于‘SQL JOINS'的解释图，如若侵犯了你的权益，请劳烦告知删除，谢谢。

![img](../media/pictures/Microservice.assets/701942-20151210224510246-264811072.png)

 

 

**2. WHERE**

对VT1过程中生成的临时表进行过滤，满足WHERE子句的列被插入到VT2表中。

注意：

此时因为分组，不能使用聚合运算；也不能使用SELECT中创建的别名；

与ON的区别：

如果有外部列，ON针对过滤的是关联表，主表（保留表）会返回所有的列；

如果没有添加外部列，两者的效果是一样的；

应用：

对主表的过滤应该放在WHERE；

对于关联表，先条件查询后连接则用ON，先连接后条件查询则用WHERE；

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> *
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike';
+-----+------+------+------+
| uid | name | oid  | uid  |
+-----+------+------+------+
| aaa | mike |    1 | aaa  |
| aaa | mike |    2 | aaa  |
| ccc | mike |    6 | ccc  |
| ddd | mike | NULL | NULL |
+-----+------+------+------+
4 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**3. GROUP BY**

这个子句会把VT2中生成的表按照GROUP BY中的列进行分组。生成VT3表。

注意：

其后处理过程的语句，如SELECT,HAVING，所用到的列必须包含在GROUP BY中，对于没有出现的，得用聚合函数；

原因：

GROUP BY改变了对表的引用，将其转换为新的引用方式，能够对其进行下一级逻辑操作的列会减少；

我的理解是：

根据分组字段，将具有相同分组字段的记录归并成一条记录，因为每一个分组只能返回一条记录，除非是被过滤掉了，而不在分组字段里面的字段可能会有多个值，多个值是无法放进一条记录的，所以必须通过聚合函数将这些具有多值的列转换成单值；

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> *
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike'
    -> GROUP BY
    -> a.uid;
+-----+------+------+------+
| uid | name | oid  | uid  |
+-----+------+------+------+
| aaa | mike |    1 | aaa  |
| ccc | mike |    6 | ccc  |
| ddd | mike | NULL | NULL |
+-----+------+------+------+
3 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**4. HAVING**

这个子句对VT3表中的不同的组进行过滤，只作用于分组后的数据，满足HAVING条件的子句被加入到VT4表中。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> *
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike'
    -> GROUP BY
    -> a.uid
    -> HAVING
    -> count(b.oid) < 2;
+-----+------+------+------+
| uid | name | oid  | uid  |
+-----+------+------+------+
| ccc | mike |    6 | ccc  |
| ddd | mike | NULL | NULL |
+-----+------+------+------+
2 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**5. SELECT**

这个子句对SELECT子句中的元素进行处理，生成VT5表。

(5-J1)计算表达式 计算SELECT 子句中的表达式，生成VT5-J1

(5-J2)DISTINCT

寻找VT5-1中的重复列，并删掉，生成VT5-J2

如果在查询中指定了DISTINCT子句，则会创建一张内存临时表（如果内存放不下，就需要存放在硬盘了）。这张临时表的表结构和上一步产生的虚拟表VT5是一样的，不同的是对进行DISTINCT操作的列增加了一个唯一索引，以此来除重复数据。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> a.uid,
    -> count(b.oid) AS total
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike'
    -> GROUP BY
    -> a.uid
    -> HAVING
    -> count(b.oid) < 2;
+-----+-------+
| uid | total |
+-----+-------+
| ccc |     1 |
| ddd |     0 |
+-----+-------+
2 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**6.ORDER BY**

从VT5-J2中的表中，根据ORDER BY 子句的条件对结果进行排序，生成VT6表。

注意：

唯一可使用SELECT中别名的地方；

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> a.uid,
    -> count(b.oid) AS total
    -> FROM
    -> table1 AS a
    -> LEFT OUTER JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike'
    -> GROUP BY
    -> a.uid
    -> HAVING
    -> count(b.oid) < 2
    -> ORDER BY
    -> total DESC;
+-----+-------+
| uid | total |
+-----+-------+
| ccc |     1 |
| ddd |     0 |
+-----+-------+
2 rows in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

**7.LIMIT**

LIMIT子句从上一步得到的VT6虚拟表中选出从指定位置开始的指定行数据。

注意：

offset和rows的正负带来的影响；

当偏移量很大时效率是很低的，可以这么做：

采用子查询的方式优化，在子查询里先从索引获取到最大id，然后倒序排，再取N行结果集

采用INNER JOIN优化，JOIN子句里也优先从索引获取ID列表，然后直接关联查询获得最终结果

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mysql> SELECT
    -> a.uid,
    -> count(b.oid) AS total
    -> FROM
    -> table1 AS a
    -> LEFT JOIN table2 AS b ON a.uid = b.uid
    -> WHERE
    -> a. NAME = 'mike'
    -> GROUP BY
    -> a.uid
    -> HAVING
    -> count(b.oid) < 2
    -> ORDER BY
    -> total DESC
    -> LIMIT 1;
+-----+-------+
| uid | total |
+-----+-------+
| ccc |     1 |
+-----+-------+
1 row in set (0.00 sec)

```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

至此SQL的解析之旅就结束了，上图总结一下：

![img](../media/pictures/Microservice.assets/701942-20151210224616246-320415795.png)

 

**参考书籍：**

《MySQL性能调优与架构实践》

《MySQL技术内幕：SQL编程》

 

**尾声：**

　　嗯，到这里这一次的深入了解之旅就差不多真的结束了，虽然也不是很深入，只是一些东西将其东拼西凑在一起而已，参考了一些以前看过的书籍，大师之笔果然不一样。而且在这过程中也是get到了蛮多东西的，最重要的是更进一步意识到，计算机软件世界的宏大呀~

　　另由于本人才疏学浅，其中难免存在纰漏错误之处，若发现劳烦告知修改，感谢~

 　　如需转载，请保留AnnsShadoW和本文地址http://www.cnblogs.com/annsshadow/p/5037667.html

## (4).索引

​	**分类：**
​		主键索引：  不能重复。id    不能是null
​		唯一索引  ：不能重复。id    可以是null
​		单值索引  ： 单列， age ;一个表可以多个单值索引,name。
​		复合索引  ：多个列构成的索引 （相当于 二级目录 ：  z: zhao）  (name,age)   (a,b,c,d,...,n)
​	**创建索引：**

方式一：

​		建索引语句:

​		**create 索引类型  索引名  on 表(字段)**
​		单值：
​		create index   dept_index on  tb(dept);

实际操作 : 这是数据库中的一个表,mybatis中的!现在要给gender加一个索引!

![1571325816258](../media/pictures/Microservice.assets/1571325816258.png)

对应的语句是:

```sql
create index  gender_index on `user`(gender)

```

![1571326035941](../media/pictures/Microservice.assets/1571326035941.png)

这里的gender_index是索引的名字! 这里的 user的是这个数据库中的表名叫user,gender这一个是要加索引的列!		



唯一：

​		create **unique** index  name_index on tb(name) ;
​		复合索引
​		create index dept_name_index on tb(dept,name);

方式二：alter table 表名 索引类型  索引名（字段）
	

```
单值：
alter table tb add index dept_index(dept) ;
唯一：
alter table tb add unique index name_index(name);
复合索引
alter table tb add index dept_name_index(dept,name);

```

​	注意：如果一个字段是primary key，则改字段默认就是 主键索引	

​	删除索引：
​	drop index 索引名 on 表名 ;
​	drop index name_index on tb ;

​	查询索引：
​	show index from 表名 ;
​	show index from 表名 \G

## (5).SQL性能问题

​	a.分析SQL的执行计划  : explain   ，可以模拟SQL优化器执行SQL语句，从而让开发人员 知道自己编写的SQL状况
​	b.MySQL查询优化其会干扰我们的优化

```
优化方法，官网：https://dev.mysql.com/doc/refman/5.5/en/optimization.html

```

​	
​	查询执行计划：  explain +SQL语句
​			explain  select  * from tb ;

 id : 编号				
 select_type ：查询类型
 table ：表
 type   ：类型
 possible_keys ：预测用到的索引 
 key  ：实际使用的索引
 key_len ：实际使用索引的长度     
 ref  :表之间的引用
 rows ：通过索引查询到的数据量 
 Extra     :额外的信息

准备数据：
create table course
(
cid int(3),
cname varchar(20),
tid int(3)
);
create table teacher
(
tid int(3),
tname varchar(20),
tcid int(3)
);

create table teacherCard
(
tcid int(3),
tcdesc varchar(200)
);

insert into course values(1,'java',1);
insert into course values(2,'html',1);
insert into course values(3,'sql',2);
insert into course values(4,'web',3);

insert into teacher values(1,'tz',1);
insert into teacher values(2,'tw',2);
insert into teacher values(3,'tl',3);

insert into teacherCard values(1,'tzdesc') ;
insert into teacherCard values(2,'twdesc') ;
insert into teacherCard values(3,'tldesc') ;

查询课程编号为2  或 教师证编号为3  的老师信息
explain +sql:
(1)id: id值相同，从上往下 顺序执行。  t3-tc3-c4

```
			  tc3--c4-t6

```

表的执行顺序  因数量的个数改变而改变的原因： 笛卡儿积

```
	a 	 b  	 c
	4	3	 2   =  			2*3=6 * 4   =24
							3*4=12* 2   =24

```

数据小的表 优先查询；



id值不同：id值越大越优先查询 (本质：在嵌套子查询时，先查内层 再查外层)

查询教授SQL课程的老师的描述（desc）
explain select tc.tcdesc from teacherCard tc,course c,teacher t where c.tid = t.tid
and t.tcid = tc.tcid and c.cname = 'sql' ;

将以上 多表查询 转为子查询形式：

explain select tc.tcdesc from teacherCard tc where tc.tcid = 
(select t.tcid from teacher t where  t.tid =  
	(select c.tid from course c where c.cname = 'sql')
);

子查询+多表： 
explain select t.tname ,tc.tcdesc from teacher t,teacherCard tc where t.tcid= tc.tcid
and t.tid = (select c.tid from course c where cname = 'sql') ;

id值有相同，又有不同： id值越大越优先；id值相同，从上往下 顺序执行

(2)select_type:查询类型
PRIMARY:包含子查询SQL中的 主查询 （最外层）
SUBQUERY：包含子查询SQL中的 子查询 （非最外层）
simple:简单查询（不包含子查询、union）
derived:衍生查询(使用到了临时表)
	a.在from子查询中只有一张表
		explain select  cr.cname 	from ( select * from course where tid in (1,2) ) cr ;

```
b.在from子查询中， 如果有table1 union table2 ，则table1 就是derived,table2就是union
	explain select  cr.cname 	from ( select * from course where tid = 1  union select * from course where tid = 2 ) cr ;

```

union:上例
union result :告知开发人员，那些表之间存在union查询

system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL



(3)type:索引类型、类型
	system>const>eq_ref>ref>range>index>all   ，要对type进行优化的前提：有索引

其中：system,const只是理想情况；实际能达到 ref>range

system（忽略）: 只有一条数据的系统表 ；或 衍生表只有一条数据的主查询
	
create table test01
(
	tid int(3),
	tname varchar(20)
);

insert into test01 values(1,'a') ;
commit;
增加索引
alter table test01 add constraint tid_pk primary key(tid) ;
explain select * from (select * from test01 )t where tid =1 ;

const:仅仅能查到一条数据的SQL ,用于Primary key 或unique索引  （类型 与索引类型有关）
explain select tid from test01 where tid =1 ;
alter table test01 drop primary key ;
create index test01_index on test01(tid) ;

eq_ref:唯一性索引：对于每个索引键的查询，返回匹配唯一行数据（有且只有1个，不能多 、不能0）
select ... from ..where name = ... .常见于唯一索引 和主键索引。

 alter table teacherCard add constraint pk_tcid primary key(tcid);
alter table teacher add constraint uk_tcid unique index(tcid) ;

explain select t.tcid from teacher t,teacherCard tc where t.tcid = tc.tcid ;

以上SQL，用到的索引是 t.tcid,即teacher表中的tcid字段；
如果teacher表的数据个数 和 连接查询的数据个数一致（都是3条数据），则有可能满足eq_ref级别；否则无法满足。

ref：非唯一性索引，对于每个索引键的查询，返回匹配的所有行（0，多）
准备数据：
 insert into teacher values(4,'tz',4) ;
 insert into teacherCard values(4,'tz222');

测试：
alter table teacher add index index_name (tname) ;
explain select * from teacher 	where tname = 'tz';

range：检索指定范围的行 ,where后面是一个范围查询(between   ,> < >=,     特殊:in有时候会失效 ，从而转为 无索引all)
alter table teacher add index tid_index (tid) ;
explain select t.* from teacher t where t.tid in (1,2) ;
explain select t.* from teacher t where t.tid <3 ;



index：查询全部索引中数据
explain select tid from teacher ; --tid 是索引， 只需要扫描索引表，不需要所有表中的所有数据

all：查询全部表中的数据
explain select cid from course ;  --cid不是索引，需要全表所有，即需要所有表中的所有数据

system/const: 结果只有一条数据
eq_ref:结果多条；但是每条数据是唯一的 ；
ref：结果多条；但是每条数据是是0或多条 ；

（4）possible_keys ：可能用到的索引，是一种预测，不准。

alter table  course add index cname_index (cname);

explain select t.tname ,tc.tcdesc from teacher t,teacherCard tc
 where t.tcid= tc.tcid
and t.tid = (select c.tid from course c where cname = 'sql') ;

如果 possible_key/key是NULL，则说明没用索引

explain select tc.tcdesc from teacherCard tc,course c,teacher t where c.tid = t.tid
and t.tcid = tc.tcid and c.cname = 'sql' ;

（5） key ：实际使用到的索引

（6）key_len ：索引的长度 ;
    作用：用于判断复合索引是否被完全使用  （a,b,c）。
create table test_kl
(
	name char(20) not null default ''
);
alter table test_kl add index index_name(name) ;
explain select * from test_kl where name ='' ;   -- key_len :60
在utf8：1个字符站3个字节  

alter table test_kl add column name1 char(20) ;  --name1可以为null

alter table test_kl add index index_name1(name1) ;
explain select * from test_kl where name1 ='' ; 
--如果索引字段可以为Null,则会使用1个字节用于标识。

drop index index_name on test_kl ;
drop index index_name1 on test_kl ;

增加一个复合索引 
alter table test_kl add index name_name1_index (name,name1) ; 

explain select * from test_kl where name1 = '' ; --121
explain select * from test_kl where name = '' ; --60

varchar(20)
alter table test_kl add column name2 varchar(20) ; --可以为Null 
alter table test_kl add index name2_index (name2) ;

explain select * from test_kl where name2 = '' ;  --63
20*3=60 +  1(null)  +2(用2个字节 标识可变长度)  =63

utf8:1个字符3个字节
gbk:1个字符2个字节
latin:1个字符1个字节

(7) ref : 注意与type中的ref值区分。
	作用： 指明当前表所 参照的 字段。
		select ....where a.c = b.x ;(其中b.x可以是常量，const)

alter table course  add index tid_index (tid) ;

```
explain select * from course c,teacher t where c.tid = t.tid  and t.tname ='tw' ;

```

(8)rows: 被索引优化查询的 数据个数 (实际通过索引而查询到的 数据个数)
	explain select * from course c,teacher t  where c.tid = t.tid
	and t.tname = 'tz' ;

（9）Extra：
	(i).using filesort ： 性能消耗大；需要“额外”的一次排序（查询）  。常见于 order by 语句中。
排序：先查询

10个人 根据年龄排序。

create table test02
(
	a1 char(3),
	a2 char(3),
	a3 char(3),
	index idx_a1(a1),
	index idx_a2(a2),
	index idx_a3(a3)
);

explain select * from test02 where a1 ='' order by a1 ;

a1:姓名  a2：年龄

explain select * from test02 where a1 ='' order by a2 ; --using filesort
小结：对于单索引， 如果排序和查找是同一个字段，则不会出现using filesort；如果排序和查找不是同一个字段，则会出现using filesort；
	避免： where哪些字段，就order by那些字段2

复合索引：不能跨列（最佳左前缀）
drop index idx_a1 on test02;
drop index idx_a2 on test02;
drop index idx_a3 on test02;

alter table test02 add index idx_a1_a2_a3 (a1,a2,a3) ;
explain select *from test02 where a1='' order by a3 ;  --using filesort
explain select *from test02 where a2='' order by a3 ; --using filesort
explain select *from test02 where a1='' order by a2 ;
explain select *from test02 where a2='' order by a1 ; --using filesort
	小结：避免： where和order by 按照复合索引的顺序使用，不要跨列或无序使用。

```
(ii). using temporary:性能损耗大 ，用到了临时表。一般出现在group by 语句中。
explain select a1 from test02 where a1 in ('1','2','3') group by a1 ;
explain select a1 from test02 where a1 in ('1','2','3') group by a2 ; --using temporary
避免：查询那些列，就根据那些列 group by .

(iii). using index :性能提升; 索引覆盖（覆盖索引）。原因：不读取原文件，只从索引文件中获取数据 （不需要回表查询）
	只要使用到的列 全部都在索引中，就是索引覆盖using index

例如：test02表中有一个复合索引(a1,a2,a3)
	explain select a1,a2 from test02 where a1='' or a2= '' ; --using index   
	
	drop index idx_a1_a2_a3 on test02;

	alter table test02 add index idx_a1_a2(a1,a2) ;
	explain select a1,a3 from test02 where a1='' or a3= '' ;

```

​		
​		如果用到了索引覆盖(using index时)，会对 possible_keys和key造成影响：
​		a.如果没有where，则索引只出现在key中；
​		b.如果有where，则索引 出现在key和possible_keys中。
​	
​		explain select a1,a2 from test02 where a1='' or a2= '' ;
​		explain select a1,a2 from test02  ;
​	
​	(iii).using where （需要回表查询）
​		假设age是索引列
​		但查询语句select age,name from ...where age =...,此语句中必须回原表查Name，因此会显示using where.
​		
​	explain select a1,a3 from test02 where a3 = '' ; --a3需要回原表查询

```
(iv). impossible where ： where子句永远为false
	explain select * from test02 where a1='x' and a1='y'  ;

```

## (6).优化案例

​	单表优化、两表优化、三表优化
​	（1）单表优化
create table book
(
​	bid int(4) primary key,
​	name varchar(20) not null,
​	authorid int(4) not null,
​	publicid int(4) not null,
​	typeid int(4) not null 
);

insert into book values(1,'tjava',1,1,2) ;
insert into book values(2,'tc',2,1,2) ;
insert into book values(3,'wx',3,2,1) ;
insert into book values(4,'math',4,2,3) ;	
commit;	

```
查询authorid=1且 typeid为2或3的	bid
explain select bid from book where typeid in(2,3) and authorid=1  order by typeid desc ;

(a,b,c)
(a,b)

优化：加索引
alter table book add index idx_bta (bid,typeid,authorid);

索引一旦进行 升级优化，需要将之前废弃的索引删掉，防止干扰。
drop index idx_bta on book;

根据SQL实际解析的顺序，调整索引的顺序：
alter table book add index idx_tab (typeid,authorid,bid); --虽然可以回表查询bid，但是将bid放到索引中 可以提升使用using index ;

再次优化（之前是index级别）：思路。因为范围查询in有时会实现，因此交换 索引的顺序，将typeid in(2,3) 放到最后。
drop index idx_tab on book;
alter table book add index idx_atb (authorid,typeid,bid);
explain select bid from book where  authorid=1 and  typeid in(2,3) order by typeid desc ;

```

​	
​	--小结：	a.最佳做前缀，保持索引的定义和使用的顺序一致性  b.索引需要逐步优化  c.将含In的范围查询 放到where条件的最后，防止失效。
​	
​	本例中同时出现了Using where（需要回原表）; Using index（不需要回原表）：原因，where  authorid=1 and  typeid in(2,3)中authorid在索引(authorid,typeid,bid)中，因此不需要回原表（直接在索引表中能查到）；而typeid虽然也在索引(authorid,typeid,bid)中，但是含in的范围查询已经使该typeid索引失效，因此相当于没有typeid这个索引，所以需要回原表（using where）；
​	例如以下没有了In，则不会出现using where
​	explain select bid from book where  authorid=1 and  typeid =3 order by typeid desc ;
​	
​	还可以通过key_len证明In可以使索引失效。
​	
​	（2）两表优化

create table teacher2
(
	tid int(4) primary key,
	cid int(4) not null
);

insert into teacher2 values(1,2);
insert into teacher2 values(2,1);
insert into teacher2 values(3,3);

create table course2
(
	cid int(4) ,
	cname varchar(20)
);

insert into course2 values(1,'java');
insert into course2 values(2,'python');
insert into course2 values(3,'kotlin');
commit;

左连接：
	explain select *from teacher2 t left outer join course2 c
	on t.cid=c.cid where c.cname='java';
	  

```
索引往哪张表加？   -小表驱动大表  
	          -索引建立经常使用的字段上 （本题 t.cid=c.cid可知，t.cid字段使用频繁，因此给该字段加索引） [一般情况对于左外连接，给左表加索引；右外连接，给右表加索引]
小表：10
大表：300
where   小表.x 10 = 大表.y 300;  --循环了几次？10
	
	大表.y 300=小表.x 10	--循环了300次

```

```
小表:10
大表:300

select ...where 小表.x10=大表.x300 ;
for(int i=0;i<小表.length10;i++)
{
	for(int j=0;j<大表.length300;j++)
	{
		...
	}
}

```

```
select ...where 大表.x300=小表.x10 ;
for(int i=0;i<大表.length300;i++)
{
	for(int j=0;j<小表.length10;j++)
	{
		...
	}
}

```

--以上2个FOR循环，最终都会循环3000次；但是 对于双层循环来说：一般建议 将数据小的循环 放外层；数据大的循环放内存。



```
--当编写 ..on t.cid=c.cid 时，将数据量小的表 放左边（假设此时t表数据量小）

alter table teacher2 add index index_teacher2_cid(cid) ;
alter table course2 add index index_course2_cname(cname);

```

```
Using join buffer:extra中的一个选项，作用：Mysql引擎使用了 连接缓存。

```

（3）三张表优化A B C
	a.小表驱动大表  b.索引建立在经常查询的字段上

示例：
create table test03
(
  a1 int(4) not null,
  a2 int(4) not null,
  a3 int(4) not null,
  a4 int(4) not null
);
alter table test03 add index idx_a1_a2_a3_4(a1,a2,a3,a4) ;

```
explain select a1,a2,a3,a4 from test03 where a1=1 and a2=2 and a3=3 and a4 =4 ; --推荐写法，因为 索引的使用顺序（where后面的顺序） 和 复合索引的顺序一致

explain select a1,a2,a3,a4 from test03 where a4=1 and a3=2 and a2=3 and a1 =4 ; --虽然编写的顺序 和索引顺序不一致，但是 sql在真正执行前 经过了SQL优化器的调整，结果与上条SQL是一致的。
--以上 2个SQL，使用了 全部的复合索引

explain select a1,a2,a3,a4 from test03 where a1=1 and a2=2 and a4=4 order by a3; 
--以上SQL用到了a1 a2两个索引，该两个字段 不需要回表查询using index ;而a4因为跨列使用，造成了该索引失效，需要回表查询 因此是using where；以上可以通过 key_len进行验证

explain select a1,a2,a3,a4 from test03 where a1=1 and a4=4 order by a3; 
--以上SQL出现了 using filesort(文件内排序，“多了一次额外的查找/排序”) ：不要跨列使用( where和order by 拼起来，不要跨列使用)

```

```
explain select a1,a2,a3,a4 from test03 where a1=1 and a4=4 order by a2 , a3; --不会using filesort

```

​	
​	--总结：i.如果 (a,b,c,d)复合索引  和使用的顺序全部一致(且不跨列使用)，则复合索引全部使用。如果部分一致(且不跨列使用)，则使用部分索引。
​	select a,c where  a = and b= and d= 
​		ii.where和order by 拼起来，不要跨列使用 

​	
​	using temporary:需要额外再多使用一张表. 一般出现在group by语句中；已经有表了，但不适用，必须再来一张表。
解析过程：			
from .. on.. join ..where ..group by ....having ...select dinstinct ..order by limit ...
​	a.
​		explain select * from test03 where a2=2 and a4=4 group by a2,a4 ;--没有using temporary
​	b.
​		explain select * from test03 where a2=2 and a4=4 group by a3 ;

## (7).避免索引失效的一些原则 

​	（1）复合索引
​	a.复合索引，不要跨列或无序使用（最佳左前缀）
​	(a,b,c)  
​	b.复合索引，尽量使用全索引匹配
​	(a,b,c)  
​	（2）不要在索引上进行任何操作（计算、函数、类型转换），否则索引失效
​		select ..where A.x = .. ;  --假设A.x是索引
​		不要：select ..where A.x*3 = .. ;
​		explain select * from book where authorid = 1 and typeid = 2 ;--用到了at2个索引
​		explain select * from book where authorid = 1 and typeid*2 = 2 ;--用到了a1个索引
​		explain select * from book where authorid*2 = 1 and typeid*2 = 2 ;----用到了0个索引
​		explain select * from book where authorid*2 = 1 and typeid = 2 ;----用到了0个索引,原因：对于复合索引，如果左边失效，右侧全部失效。(a,b,c)，例如如果 b失效，则b c同时失效。
​	
 		drop index idx_atb on book ; 
​		alter table book add index idx_authroid (authorid) ;
​		alter table book add index idx_typeid (typeid) ;
​		explain select * from book where authorid*2 = 1 and typeid = 2 ;
​	（3）复合索引不能使用不等于（!=  <>）或is null (is not null)，否则自身以及右侧所有全部失效。
​		复合索引中如果有>，则自身和右侧索引全部失效。

```
explain select * from book where authorid = 1 and typeid =2 ;

-- SQL优化，是一种概率层面的优化。至于是否实际使用了我们的优化，需要通过explain进行推测。

explain select * from book where authorid != 1 and typeid =2 ;
explain select * from book where authorid != 1 and typeid !=2 ;

```

​	
​	体验概率情况(< > =)：原因是服务层中有SQL优化器，可能会影响我们的优化。
​	drop index idx_typeid on book;
​	drop index idx_authroid on book;
​	alter table book add index idx_book_at (authorid,typeid);
​	explain select * from book where authorid = 1 and typeid =2 ;--复合索引at全部使用
​	explain select * from book where authorid > 1 and typeid =2 ; --复合索引中如果有>，则自身和右侧索引全部失效。
​	explain select * from book where authorid = 1 and typeid >2 ;--复合索引at全部使用
​	----明显的概率问题---
​	explain select * from book where authorid < 1 and typeid =2 ;--复合索引at只用到了1个索引
​	explain select * from book where authorid < 4 and typeid =2 ;--复合索引全部失效
​	
​	--我们学习索引优化 ，是一个大部分情况适用的结论，但由于SQL优化器等原因  该结论不是100%正确。
​	--一般而言， 范围查询（> <  in），之后的索引失效。
​	
​	（4）补救。尽量使用索引覆盖（using index）
​			（a,b,c）
​	select a,b,c from xx..where a=  .. and b =.. ;
​	
​	(5) like尽量以“常量”开头，不要以'%'开头，否则索引失效
​	select * from xx where name like '%x%' ; --name索引失效
​	
​	explain select * from teacher  where tname like '%x%'; --tname索引失效
​	
​	explain select * from teacher  where tname like 'x%';
​	 
​	explain select tname from teacher  where tname like '%x%'; --如果必须使用like '%x%'进行模糊查询，可以使用索引覆盖 挽救一部分。

```
（6）尽量不要使用类型转换（显示、隐式），否则索引失效
explain select * from teacher where tname = 'abc' ;
explain select * from teacher where tname = 123 ;//程序底层将 123 -> '123'，即进行了类型转换，因此索引失效

（7）尽量不要使用or，否则索引失效
explain select * from teacher where tname ='' or tcid >1 ; --将or左侧的tname 失效。

```

## (8).一些其他的优化方法

​	（1）
​	exist和in
​	select ..from table where exist (子查询) ;
​	select ..from table where 字段 in  (子查询) ;

```
如果主查询的数据集大，则使用In   ,效率高。
如果子查询的数据集大，则使用exist,效率高。	

exist语法： 将主查询的结果，放到子查需结果中进行条件校验（看子查询是否有数据，如果有数据 则校验成功）  ，
	    如果 复合校验，则保留数据；

select tname from teacher where exists (select * from teacher) ; 
--等价于select tname from teacher

```

​	
​	select tname from teacher where exists (select * from teacher where tid =9999) ;
​	
​	in:
​	select ..from table where tid in  (1,3,5) ;

```
（2）order by 优化
using filesort 有两种算法：双路排序、单路排序 （根据IO的次数）
MySQL4.1之前 默认使用 双路排序；双路：扫描2次磁盘（1：从磁盘读取排序字段 ,对排序字段进行排序（在buffer中进行的排序）   2：扫描其他字段 ）
	--IO较消耗性能
MySQL4.1之后 默认使用 单路排序  ： 只读取一次（全部字段），在buffer中进行排序。但种单路排序 会有一定的隐患 （不一定真的是“单路|1次IO”，有可能多次IO）。原因：如果数据量特别大，则无法 将所有字段的数据 一次性读取完毕，因此 会进行“分片读取、多次读取”。
	注意：单路排序 比双路排序 会占用更多的buffer。
		单路排序在使用时，如果数据大，可以考虑调大buffer的容量大小：  set max_length_for_sort_data = 1024  单位byte

如果max_length_for_sort_data值太低，则mysql会自动从 单路->双路   （太低：需要排序的列的总大小超过了max_length_for_sort_data定义的字节数）

提高order by查询的策略：
a.选择使用单路、双路 ；调整buffer的容量大小；
b.避免select * ...  
c.复合索引 不要跨列使用 ，避免using filesort
d.保证全部的排序字段 排序的一致性（都是升序 或 降序）

```

​	

## (9).SQL排查 - 慢查询日志:MySQL提供的一种日志记录，用于记录MySQL种响应时间超过阀值的SQL语句 （long_query_time，默认10秒）

​		慢查询日志默认是关闭的；建议：开发调优是 打开，而 最终部署时关闭。
​	

```
检查是否开启了 慢查询日志 ：   show variables like '%slow_query_log%' ;

临时开启：
	set global slow_query_log = 1 ;  --在内存种开启
	exit
	service mysql restart

永久开启：
	/etc/my.cnf 中追加配置：
	vi /etc/my.cnf 
	[mysqld]
	slow_query_log=1
	slow_query_log_file=/var/lib/mysql/localhost-slow.log

```

​	
​	慢查询阀值：
​		show variables like '%long_query_time%' ;
​	
​	临时设置阀值：
​		set global long_query_time = 5 ; --设置完毕后，重新登陆后起效 （不需要重启服务）
​	
​	永久设置阀值：
​			
​		/etc/my.cnf 中追加配置：
​		vi /etc/my.cnf 
​		[mysqld]
​		long_query_time=3

```
select sleep(4);
select sleep(5);
select sleep(3);
select sleep(3);
--查询超过阀值的SQL：  show global status like '%slow_queries%' ;

(1)慢查询的sql被记录在了日志中，因此可以通过日志 查看具体的慢SQL。
cat /var/lib/mysql/localhost-slow.log

(2)通过mysqldumpslow工具查看慢SQL,可以通过一些过滤条件 快速查找出需要定位的慢SQL
mysqldumpslow --help
s：排序方式
r:逆序
l:锁定时间
g:正则匹配模式		

```

```
--获取返回记录最多的3个SQL
	mysqldumpslow -s r -t 3  /var/lib/mysql/localhost-slow.log

--获取访问次数最多的3个SQL
	mysqldumpslow -s c -t 3 /var/lib/mysql/localhost-slow.log

--按照时间排序，前10条包含left join查询语句的SQL
	mysqldumpslow -s t -t 10 -g "left join" /var/lib/mysql/localhost-slow.log

语法：
	mysqldumpslow 各种参数  慢查询日志的文件

```

## (10).分析海量数据

```
a.模拟海量数据  存储过程（无return）/存储函数（有return）
create database testdata ;
use testdata

```

create table dept
(
dno int(5) primary key default 0,
dname varchar(20) not null default '',
loc varchar(30) default ''
)engine=innodb default charset=utf8;

create table emp
(
eid int(5) primary key,
ename varchar(20) not null default '',
job varchar(20) not null default '',
deptno int(5) not null default 0
)engine=innodb default charset=utf8;
	通过存储函数 插入海量数据：
	创建存储函数：
		randstring(6)  ->aXiayx  用于模拟员工名称

```
delimiter $ 
create function randstring(n int)   returns varchar(255) 
begin
	declare  all_str varchar(100) default 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ' ;
	declare return_str varchar(255) default '' ;
	declare i int default 0 ; 
	while i<n		 
	do									
		set return_str = concat(  return_str,      substring(all_str,   FLOOR(1+rand()*52)   ,1)       );
		set i=i+1 ;
	end while ;
	return return_str;
	
end $ 

```

--如果报错：You have an error in your SQL syntax，说明SQL语句语法有错，需要修改SQL语句；

 如果报错This function has none of DETERMINISTIC, NO SQL, or READS SQL DATA in its declaration and binary logging is enabled (you *might* want to use the less safe log_bin_trust_function_creators variable)
	是因为 存储过程/存储函数在创建时 与之前的 开启慢查询日志冲突了 
	解决冲突：
	临时解决( 开启log_bin_trust_function_creators )
		show variables like '%log_bin_trust_function_creators%';
		set global log_bin_trust_function_creators = 1;
	永久解决：
	/etc/my.cnf 
	[mysqld]
	log_bin_trust_function_creators = 1

```
--产生随机整数
create function ran_num() returns int(5)
begin
	declare i int default 0;
	set i =floor( rand()*100 ) ;
	return i ;

end $

```



```
--通过存储过程插入海量数据：emp表中  ，  10000,   100000
create procedure insert_emp( in eid_start int(10),in data_times int(10))
begin 
	declare i int default 0;
	set autocommit = 0 ;
	
	repeat
		
		insert into emp values(eid_start + i, randstring(5) ,'other' ,ran_num()) ;
		set i=i+1 ;
		until i=data_times
	end repeat ;
	commit ;
end $

```

```
--通过存储过程插入海量数据：dept表中  
	create procedure insert_dept(in dno_start int(10) ,in data_times int(10))
	begin
		declare i int default 0;
		set autocommit = 0 ;
		repeat
		
			insert into dept values(dno_start+i ,randstring(6),randstring(8)) ;
			set i=i+1 ;
			until i=data_times
		end repeat ;
	commit ;

```

```
	end$

```

```
--插入数据
	delimiter ; 
	call insert_emp(1000,800000) ;
	call insert_dept(10,30) ;

```

​	
​	b.分析海量数据:
​	（1）profiles
​	show profiles ; --默认关闭
​	show variables like '%profiling%';
​	set profiling = on ; 
​	show profiles  ：会记录所有profiling打开之后的  全部SQL查询语句所花费的时间。缺点：不够精确，只能看到 总共消费的时间，不能看到各个硬件消费的时间（cpu  io ）
​	
​	(2)--精确分析:sql诊断
​	 show profile all for query 上一步查询的的Query_Id
​	 show profile cpu,block io for query 上一步查询的的Query_Id
​	
​	(3)全局查询日志 ：记录开启之后的 全部SQL语句。 （这次全局的记录操作 仅仅在调优、开发过程中打开即可，在最终的部署实施时 一定关闭）
​		show variables like '%general_log%';
​		
​		--执行的所有SQL记录在表中
​		set global general_log = 1 ;--开启全局日志
​		set global log_output='table' ; --设置 将全部的SQL 记录在表中
​	
​		--执行的所有SQL记录在文件中
​		set global log_output='file' ;
​		set global general_log = on ;
​		set global general_log_file='/tmp/general.log' ;

```
	开启后，会记录所有SQL ： 会被记录 mysql.general_log表中。
		select * from  mysql.general_log ;

```

## (11).锁机制 ：解决因资源共享 而造成的并发问题。

​	示例：买最后一件衣服X
​	A:  	X	买 ：  X加锁 ->试衣服...下单..付款..打包 ->X解锁
​	B:	X       买：发现X已被加锁，等待X解锁，   X已售空

```
分类：
操作类型：
	a.读锁（共享锁）： 对同一个数据（衣服），多个读操作可以同时进行，互不干扰。
	b.写锁（互斥锁）： 如果当前写操作没有完毕（买衣服的一系列操作），则无法进行其他的读操作、写操作

操作范围：
	a.表锁 ：一次性对一张表整体加锁。如MyISAM存储引擎使用表锁，开销小、加锁快；无死锁；但锁的范围大，容易发生锁冲突、并发度低。
	b.行锁 ：一次性对一条数据加锁。如InnoDB存储引擎使用行锁，开销大，加锁慢；容易出现死锁；锁的范围较小，不易发生锁冲突，并发度高（很小概率 发生高并发问题：脏读、幻读、不可重复度、丢失更新等问题）。
	c.页锁		

```

示例：

```
（1）表锁 ：  --自增操作 MYSQL/SQLSERVER 支持；oracle需要借助于序列来实现自增

```

create table tablelock
(
id int primary key auto_increment , 
name varchar(20)
)engine myisam;

insert into tablelock(name) values('a1');
insert into tablelock(name) values('a2');
insert into tablelock(name) values('a3');
insert into tablelock(name) values('a4');
insert into tablelock(name) values('a5');
commit;

```
增加锁：
locak table 表1  read/write  ,表2  read/write   ,...

查看加锁的表：
show open tables ;

会话：session :每一个访问数据的dos命令行、数据库客户端工具  都是一个会话

===加读锁：
	会话0：
		lock table  tablelock read ;
		select * from tablelock; --读（查），可以
		delete from tablelock where id =1 ; --写（增删改），不可以

		select * from emp ; --读，不可以
		delete from emp where eid = 1; --写，不可以
		结论1：
		--如果某一个会话 对A表加了read锁，则 该会话 可以对A表进行读操作、不能进行写操作； 且 该会话不能对其他表进行读、写操作。
		--即如果给A表加了读锁，则当前会话只能对A表进行读操作。

	会话1（其他会话）：
		select * from tablelock;   --读（查），可以
		delete from tablelock where id =1 ; --写，会“等待”会话0将锁释放

```

```
	会话1（其他会话）：
		select * from emp ;  --读（查），可以
		delete from emp where eno = 1; --写，可以
		结论2：
		--总结：
			会话0给A表加了锁；其他会话的操作：a.可以对其他表（A表以外的表）进行读、写操作
							b.对A表：读-可以；  写-需要等待释放锁。
	释放锁: unlock tables ;

```



```
===加写锁：
	会话0：
		lock table tablelock write ;

		当前会话（会话0） 可以对加了写锁的表  进行任何操作（增删改查）；但是不能 操作（增删改查）其他表
	其他会话：
		对会话0中加写锁的表 可以进行增删改查的前提是：等待会话0释放写锁

```

MySQL表级锁的锁模式
MyISAM在执行查询语句（SELECT）前，会自动给涉及的所有表加读锁，
在执行更新操作（DML）前，会自动给涉及的表加写锁。
所以对MyISAM表进行操作，会有以下情况：
a、对MyISAM表的读操作（加读锁），不会阻塞其他进程（会话）对同一表的读请求，
但会阻塞对同一表的写请求。只有当读锁释放后，才会执行其它进程的写操作。
b、对MyISAM表的写操作（加写锁），会阻塞其他进程（会话）对同一表的读和写操作，
只有当写锁释放后，才会执行其它进程的读写操作。



分析表锁定：
	查看哪些表加了锁：   show open tables ;  1代表被加了锁
	分析表锁定的严重程度： show status like 'table%' ;
			Table_locks_immediate :即可能获取到的锁数
			Table_locks_waited：需要等待的表锁数(如果该值越大，说明存在越大的锁竞争)
	一般建议：
		Table_locks_immediate/Table_locks_waited > 5000， 建议采用InnoDB引擎，否则MyISAM引擎

​	

（2）行表（InnoDB）
create table linelock(
id int(5) primary key auto_increment,
name varchar(20)
)engine=innodb ;
insert into linelock(name) values('1')  ;
insert into linelock(name) values('2')  ;
insert into linelock(name) values('3')  ;
insert into linelock(name) values('4')  ;
insert into linelock(name) values('5')  ;

--mysql默认自动commit;	oracle默认不会自动commit ;

为了研究行锁，暂时将自动commit关闭;  set autocommit =0 ; 以后需要通过commit

```
会话0： 写操作
	insert into linelock values(	'a6') ;
   
会话1： 写操作 同样的数据
	update linelock set name='ax' where id = 6;

对行锁情况：
	1.如果会话x对某条数据a进行 DML操作（研究时：关闭了自动commit的情况下），则其他会话必须等待会话x结束事务(commit/rollback)后  才能对数据a进行操作。
	2.表锁 是通过unlock tables，也可以通过事务解锁 ; 行锁 是通过事务解锁。

```

​		

```
行锁，操作不同数据：

会话0： 写操作

	insert into linelock values(8,'a8') ;
会话1： 写操作， 不同的数据
	update linelock set name='ax' where id = 5;
	行锁，一次锁一行数据；因此 如果操作的是不同数据，则不干扰。

```

```
行锁的注意事项：
a.如果没有索引，则行锁会转为表锁
show index from linelock ;
alter table linelock add index idx_linelock_name(name);

```

​	
​	会话0： 写操作
​		update linelock set name = 'ai' where name = '3' ;
​		
​	会话1： 写操作， 不同的数据
​		update linelock set name = 'aiX' where name = '4' ;

​	
​	会话0： 写操作
​		update linelock set name = 'ai' where name = 3 ;
​		
​	会话1： 写操作， 不同的数据
​		update linelock set name = 'aiX' where name = 4 ;
​		
​	--可以发现，数据被阻塞了（加锁）
​	-- 原因：如果索引类 发生了类型转换，则索引失效。 因此 此次操作，会从行锁 转为表锁。
​	
​	b.行锁的一种特殊情况：间隙锁：值在范围内，但却不存在
​	 --此时linelock表中 没有id=7的数据
​	 update linelock set name ='x' where id >1 and id<9 ;   --即在此where范围中，没有id=7的数据，则id=7的数据成为间隙。
​	间隙：Mysql会自动给 间隙 加索 ->间隙锁。即 本题 会自动给id=7的数据加 间隙锁（行锁）。
​	行锁：如果有where，则实际加索的范围 就是where后面的范围（不是实际的值）

​	
​	如何仅仅是查询数据，能否加锁？ 可以   for update 
​	研究学习时，将自动提交关闭：
​		set autocommit =0 ;
​		start transaction ;
​		begin ;
​	 select * from linelock where id =2 for update ;
​	
​	通过for update对query语句进行加锁。
​	
​	行锁：
​	InnoDB默认采用行锁；
​	缺点： 比表锁性能损耗大。
​	优点：并发能力强，效率高。
​	因此建议，高并发用InnoDB，否则用MyISAM。
​	
​	行锁分析：
​	  show status like '%innodb_row_lock%' ;
​		 Innodb_row_lock_current_waits :当前正在等待锁的数量  
​		  Innodb_row_lock_time：等待总时长。从系统启到现在 一共等待的时间
​		 Innodb_row_lock_time_avg  ：平均等待时长。从系统启到现在平均等待的时间
​		 Innodb_row_lock_time_max  ：最大等待时长。从系统启到现在最大一次等待的时间
​		 Innodb_row_lock_waits ：	等待次数。从系统启到现在一共等待的次数

## (12).主从复制  （集群在数据库的一种实现）

​	windows:mysql 主
​	linux:mysql从

```
安装windows版mysql:
	如果之前计算机中安装过Mysql，要重新再安装  则需要：先卸载 再安装
	先卸载：
		通过电脑自带卸载工具卸载Mysql (电脑管家也可以)
		删除一个mysql缓存文件C:\ProgramData\MySQL
		删除注册表regedit中所有mysql相关配置
		--重启计算机
		
	安装MYSQL：
		安装时，如果出现未响应：  则重新打开D:\MySQL\MySQL Server 5.5\bin\MySQLInstanceConfig.exe

	图形化客户端： SQLyog, Navicat

```

```
	如果要远程连接数据库，则需要授权远程访问。 
	授权远程访问 :(A->B,则再B计算机的Mysql中执行以下命令)
	GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;
	FLUSH PRIVILEGES;

	如果仍然报错：可能是防火墙没关闭 ：  在B关闭防火墙  service iptables stop 

```



```
实现主从同步（主从复制）：图
	1.master将改变的数 记录在本地的 二进制日志中（binary log） ；该过程 称之为：二进制日志件事
	2.slave将master的binary log拷贝到自己的 relay log（中继日志文件）中
	3.中继日志事件，将数据读取到自己的数据库之中
MYSQL主从复制 是异步的，串行化的， 有延迟

master:slave = 1:n

配置： 
windows(mysql: my.ini)
  linux(mysql: my.cnf)

配置前，为了无误，先将权限(远程访问)、防火墙等处理：
	关闭windows/linux防火墙： windows：右键“网络”   ,linux: service iptables stop
	Mysql允许远程连接(windowos/linux)：
		GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;
		FLUSH PRIVILEGES;

```

主机（以下代码和操作 全部在主机windows中操作）：
my.ini
[mysqld]
#id
server-id=1
#二进制日志文件（注意是/  不是\）
log-bin="D:/MySQL/MySQL Server 5.5/data/mysql-bin"
#错误记录文件
log-error="D:/MySQL/MySQL Server 5.5/data/mysql-error"
#主从同步时 忽略的数据库
binlog-ignore-db=mysql
#(可选)指定主从同步时，同步哪些数据库
binlog-do-db=test	

windows中的数据库 授权哪台计算机中的数据库 是自己的从数据库：	
 GRANT REPLICATION slave,reload,super ON *.* TO 'root'@'192.168.2.%' IDENTIFIED BY 'root';
 flush privileges ; 

```
查看主数据库的状态（每次在左主从同步前，需要观察 主机状态的最新值）
	show master status;  （mysql-bin.000001、 107）

```

从机（以下代码和操作 全部在从机linux中操作）：

my.cnf
[mysqld]
server-id=2
log-bin=mysql-bin
replicate-do-db=test

linux中的数据 授权哪台计算机中的数控 是自己的主计算机
CHANGE MASTER TO 
MASTER_HOST = '192.168.2.2', 
MASTER_USER = 'root', 
MASTER_PASSWORD = 'root', 
MASTER_PORT = 3306,
master_log_file='mysql-bin.000001',
master_log_pos=107;
	如果报错：This operation cannot be performed with a running slave; run STOP SLAVE first
	解决：STOP SLAVE ;再次执行上条授权语句

开启主从同步：
	从机linux:
	start slave ;
	检验  show slave status \G	主要观察： Slave_IO_Running和 Slave_SQL_Running，确保二者都是yes；如果不都是yes，则看下方的 Last_IO_Error。
本次 通过 Last_IO_Error发现错误的原因是 主从使用了相同的server-id， 检查:在主从中分别查看serverid:  show variables like 'server_id' ;
	可以发现，在Linux中的my.cnf中设置了server-id=2，但实际执行时 确实server-id=1，原因：可能是 linux版Mysql的一个bug，也可能是 windows和Linux版本不一致造成的兼容性问题。
	解决改bug： set global server_id =2 ;

```
stop slave ;
 set global server_id =2 ;
start slave ;
 show slave status \G

演示：
主windows =>从

windows:
将表，插入数据  
观察从数据库中该表的数据

```

数据库+后端

```
spring boot（企业级框架,目前使用较多）  

```



# 11.秒杀 jmeter

jmeter 测试系统能经受多大负载的开源jar,做性能测试的开源项目!

打开软件文件bin目录，然后点击ApacheJmeter.jar就可以打开窗口。 或者点击bin里面的jmter.bat 也可以打开软件。

![1592983096396](../media/pictures/Microservice.assets/1592983096396.png)





首先将这个软件修改成中文!

![1571379480884](../media/pictures/Microservice.assets/1571379480884.png)



## 秒杀服务之秒杀项目构建

### 秒杀项目业务场景介绍

现该电影网站和各大影院合作，推出一个购买兑换码活动。用户参与流程如下

![](../media/pictures/Microservice.assets/f79f406066dbaee85c92d5bf6be706bf.png)

注意：优惠券是限量的

## 秒杀相关概念介绍

### 库存

参与秒杀活动商品的数量

这个项目中将秒杀的库存表放在另一个单独的表里面,是因为,秒杀的时候,库存这个数据需要一直更新,而数据库中其他数据不需要动,将库存放在一个单独的表中,是为了更新库存的速度变快! 

### 超卖问题

卖出的商品的数量大于活动库存的数量

造成超卖问题的原因？

库存并发更新

## 高并发相关概念介绍

### 并发

> 同时拥有两个或多个线程，如果程序在单核处理器上运行，多个线程将交替地换入或者换出内存，这些线程是同时「
> 存在
> 」的，每个线程都处于执行过程中的某个状态，如果运行在多核处理器上，此时，程序中每个线程都将分配到一个处理器核上，因此可以同时运行。也就是说，并发就是多个线程操作相同的物理机中的资源，保证其线程安全，合理的利用资源。

### 高并发

> 由于分布式系统的问世，高并发（High
> Concurrency）通常是指通过设计保证系统能够同时并行处理很多请求。通俗来讲，高并发是指在同一个时间点，有很多用户同时的访问同一
> API 接口或者 Url
> 地址。它经常会发生在有大活跃用户量，用户高聚集的业务场景中。（百度词条）

> 高并发中有如下概念：

#### QPS（Query Per Second）

> 每秒钟处理完请求的次数；注意这里是处理完。具体是指发出请求到服务器处理完成功返回结果。可以理解在server中有个counter，每处理一个请求加1，1秒后counter=QPS。

#### TPS（Transaction Per Second）

> 一般来说是针对整个系统来说的，指每秒能够处理完的事物数，针对单个接口来说一般用QPS

#### 并发量

> 系统能够同时处理的请求数

#### 响应时间

> 系统处理一次请求所需要的平均处理时间

#### 计算关系：

QPS = 并发量 / 平均响应时间

并发量 = QPS \* 平均响应时间

### 高可用

高可用（HighAvailability）是系统架构设计中必须考虑的因素之一，它通常是指，通过设计减少系统不能提供服务的时间。计量单位是百分比，常用99%,99.9%,99.99%来表示。一般讲4个9，5个9或者6个9。

举个例子：可用性为99%的系统，全年停机时间为3.5天；99.9%的系统；全年停机时间为8.5小时；99.99%的系统全年停机时间为53分钟；99.999%的系统全年停机时间仅仅约为5分钟。

## 如何设计高并发系统

### 提高并发量

如何提高并发量？也就是提高系统能够同时处理的请求数量，例如

### 提高物理机器性能

比如：增强单机硬件性能，例如：增加CPU核数如32核，升级更好的网卡如万兆，升级更好的硬盘如SSD，扩充硬盘容量如2T，扩充系统内存如128G；

### 增加能够同时处理请求的个数：

比如：增加节点、配置tomcat线程池 等等

### 缩短平均响应时间

等于如何提高接口响应速度？

缓存、异步、无锁等等

## 高并发系统的三把利器：

缓存、限流、降级

缓存：提升系统响应速度、增大系统能够处理的容量

降级：当服务出问题或者影响到核心流程的性能则需要暂时屏蔽掉，待高峰或者问题解决后再打开

限流：限流的目的是通过对并发访问/请求进行限速或者一个时间窗口内的的请求进行限速来保护系统，一旦达到限制速率则可以拒绝服务

## Jmeter的介绍

JMeter是Apache组织开发的开源项目，设计之初是用于做性能测试的，同时它在实现对各种接口的调用方面做的比较成熟，因此，常被用做接口功能测试和性能测试。

它能够很好的支持各种常见接口，如HTTP(S)、WebService、JDBC、JAVA、FTP等，并以多种形式与参数展现测试结果。

1. Jmeter的使用
   1. 安装JDK并且配置好环境变量
   2. 安装Jmeter

其实jmeter是免安装的，只需要下载解压即可。

安装包直接去jmeter官网下载即可（[http://jmeter.apache.org/down...](http://jmeter.apache.org/download_jmeter.cgi)），建议选择3.0或以上版本，我目前使用的是5.1.1的版本。下载后解压到非C盘的非中文目录即可。

1. 如何使用Jmter
   1. 添加测试计划
   2. 添加线程组

![](../media/pictures/Microservice.assets/a4a34ad9a19aea78fab596be3ffe2735.png)

设置线程组

### 构建请求

![](../media/pictures/Microservice.assets/c85ef0a1a1f66dd79989c7212a7472cf.png)

以HTTP为例，我们需要设置以下请求参数

请求名称

协议

服务器IP/域名

端口号

HTTP请求方法、路径

添加请求参数

勾选☑️使用Keep-alive

点击高级 —\> 选择Java客户端实现

如果需要设置请求头参数，则需要点击如下设置：

![](../media/pictures/Microservice.assets/0d9aeb7c7716cdf7c57cb875b147199a.png)

### 查看结果

> 添加查看结果树

> 添加聚合报告

![](../media/pictures/Microservice.assets/219d5f0dac9538a774a4c74afe3ed55b.png)

点击上方绿色执行箭头开始测试

1. 秒杀接口业务介绍
   1. 业务表设计
   2. 业务接口

> 1、查询秒杀活动接口

> 2、秒杀下单接口

> 生成订单 扣减库存

> 如何优化？优化之后会带来什么问题？



## 秒杀接口业务介绍

### 业务表设计

### 业务接口

查询秒杀活动接口

秒杀下单接口

​              生成订单 扣减库存

如何优化？优化之后会带来什么问题？



## Linux系统上面  Load Average 

网上查到相关信息:

![1571383240086](../media/pictures/Microservice.assets/1571383240086.png)

上面的load average 是记录系统一分钟,五分钟,十五分钟的平均负载的! 后面的数字是负载

一幅图秒懂LoadAverage（负载）



一、什么是Load Average？

系统负载（System Load）是系统CPU繁忙程度的度量，即有多少进程在等待被CPU调度（进程等待队列的长度）。

平均负载（Load Average）是一段时间内系统的平均负载，这个一段时间一般取1分钟、5分钟、15分钟。



二、如何查看Load？

top命令，w命令，uptime等命令都可以查看系统负载：

[shenjian@dev02 ~]$ uptime

13:53:39 up 130 days,  2:15,  1 user,  load average: 1.58, 2.58, 5.58

如上所示，dev02机器1分钟平均负载，5分钟平均负载，15分钟平均负载分别是1.58、2.58、5.58



三、Load的数值是什么含义？

把CPU比喻成一条（单核）马路，进程任务比喻成马路上跑着的汽车，Load则表示马路的繁忙程度：

Load小于1：表示完全不堵车，汽车在马路上跑得游刃有余：

[![load0.5](../media/pictures/Microservice.assets/load0.5.png)](http://www.habadog.com/wp-content/uploads/2015/02/load0.5.png)[ Load<1，单核]

Load等于1：马路已经没有额外的资源跑更多的汽车了：

[![load1](../media/pictures/Microservice.assets/load1.png)](http://www.habadog.com/wp-content/uploads/2015/02/load1.png)[Load==1，单核]

Load大于1：汽车都堵着等待进入马路：

[![load5](../media/pictures/Microservice.assets/load5.png)](http://www.habadog.com/wp-content/uploads/2015/02/load5.png)[Load>1，单核]

如果有两个CPU，则表示有两条马路，此时即使Load大于1也不代表有汽车在等待：

[![load2](../media/pictures/Microservice.assets/load2.png)](http://www.habadog.com/wp-content/uploads/2015/02/load2.png)[Load==2，双核，没有等待]



四、什么样的Load值得警惕（单核）？

Load < 0.7时：系统很闲，马路上没什么车，要考虑多部署一些服务

0.7 < Load < 1时：系统状态不错，马路可以轻松应对

Load == 1时：系统马上要处理不多来了，赶紧找一下原因

Load > 5时：马路已经非常繁忙了，进入马路的每辆汽车都要无法很快的运行



五、三个Load值要先看哪一个？

结合具体情况具体分析：

1）1分钟Load>5，5分钟Load<1，15分钟Load<1：短期内繁忙，中长期空闲，初步判断是一个“抖动”，或者是“拥塞前兆”

2）1分钟Load>5，5分钟Load>1，15分钟Load<1：短期内繁忙，中期内紧张，很可能是一个“拥塞的开始”

3）1分钟Load>5，5分钟Load>5，15分钟Load>5：短中长期都繁忙，系统“正在拥塞”

4）1分钟Load<1，5分钟Load>1，15分钟Load>5：短期内空闲，中长期繁忙，不用紧张，系统“拥塞正在好转”



六、Load总结

[![load0.5](D:/Code/Typora/media/pictures/Microservice.assets/load0.5.png)](http://www.habadog.com/wp-content/uploads/2015/02/load0.5.png)[ Load<1，单核]

[![load1](../media/pictures/Microservice.assets/load1-1594393995126.png)](http://www.habadog.com/wp-content/uploads/2015/02/load1.png)[Load==1，单核]

[![load5](../media/pictures/Microservice.assets/load5.png)](http://www.habadog.com/wp-content/uploads/2015/02/load5.png)[Load>1，单核]

[![load2](D:/Code/Typora/media/pictures/Microservice.assets/load2.png)](http://www.habadog.com/wp-content/uploads/2015/02/load2.png)[Load==2，双核]

希望上面一幅图对大家理解Load Average有帮助，赶快uptime一下，看一下自己系统的负载吧。

# 12.消息队列(自己找的简单易懂)

## 一、什么是消息队列？

消息队列不知道大家看到这个词的时候，会不会觉得它是一个比较高端的技术，反正我是觉得它好像是挺牛逼的。

消息队列，一般我们会简称它为MQ(Message Queue)，嗯，就是很直白的简写。

我们先不管消息(Message)这个词，来看看队列(Queue)。这一看，队列大家应该都熟悉吧。

队列是一种先进先出的数据结构。

[![img](../media/pictures/Microservice.assets/ccc415ee02dac374116ffd324e079299.jpg)](https://s5.51cto.com/oss/201904/15/ccc415ee02dac374116ffd324e079299.jpg)

在Java里边，已经实现了不少的队列了：

[![img](../media/pictures/Microservice.assets/3140455cd169462a76efc1cf484e9b0b.jpg)](https://s5.51cto.com/oss/201904/15/3140455cd169462a76efc1cf484e9b0b.jpg)

那为什么还需要消息队列(MQ)这种中间件呢？？？

- 到这里，大家可以先猜猜为什么要用消息队列(MQ)这种中间件，下面会继续补充。

消息队列可以简单理解为：把要传输的数据放在队列中。

[![img](../media/pictures/Microservice.assets/8bcc9ce29559849fb30c4a8260759d36.png)](https://s2.51cto.com/oss/201904/15/8bcc9ce29559849fb30c4a8260759d36.png)

图片来源：https://www.cloudamqp.com/blog/2014-12-03-what-is-message-queuing.html

科普：

- 把数据放到消息队列叫做生产者
- 从消息队列里边取数据叫做消费者

## **二、为什么要用消息队列？**

为什么要用消息队列，也就是在问：用了消息队列有什么好处。我们看看以下的场景

**2.1 解耦**

现在我有一个系统A，系统A可以产生一个userId

[![img](../media/pictures/Microservice.assets/6684b608abe04b214b92ee17f2889c12.jpg)](https://s4.51cto.com/oss/201904/15/6684b608abe04b214b92ee17f2889c12.jpg)

然后，现在有系统B和系统C都需要这个userId去做相关的操作

[![img](../media/pictures/Microservice.assets/f66c17df010a66b1485461efe0138b77.jpg)](https://s3.51cto.com/oss/201904/15/f66c17df010a66b1485461efe0138b77.jpg)

写成伪代码可能是这样的：

```
public class SystemA {  
// 系统B和系统C的依赖      
SystemB systemB = new SystemB(); 
SystemC systemC = new SystemC();      
// 系统A独有的数据userId    
private String userId = "Java3y";    
public void doSomething() {          // 系统B和系统C都需要拿着系统A的userId去操作其他的事          systemB.SystemBNeed2do(userId);        
systemC.SystemCNeed2do(userId);     
} 
} 

```

结构图如下：

[![img](../media/pictures/Microservice.assets/357f83f657673a37d69efad5f726527b.jpg)](https://s4.51cto.com/oss/201904/15/357f83f657673a37d69efad5f726527b.jpg)

ok，一切平安无事度过了几个天。

某一天，系统B的负责人告诉系统A的负责人，现在系统B的SystemBNeed2do(String userId)这个接口不再使用了，让系统A别去调它了。

于是，系统A的负责人说"好的，那我就不调用你了。"，于是就把调用系统B接口的代码给删掉了：

```
public void doSomething() { 
// 系统A不再调用系统B的接口了  
//systemB.SystemBNeed2do(userId);    
systemC.SystemCNeed2do(userId);  
} 

```

又过了几天，系统D的负责人接了个需求，也需要用到系统A的userId，于是就跑去跟系统A的负责人说："老哥，我要用到你的userId，你调一下我的接口吧"

于是系统A说："没问题的，这就搞"

[![img](../media/pictures/Microservice.assets/ebe507302ee87c6b2d29e32b42d79ee9.jpg)](https://s1.51cto.com/oss/201904/15/ebe507302ee87c6b2d29e32b42d79ee9.jpg)

然后，系统A的代码如下：

```java
public class SystemA {  
    // 已经不再需要系统B的依赖了    
    // SystemB systemB = new SystemB();     
    // 系统C和系统D的依赖    
    SystemC systemC = new SystemC();    
    SystemD systemD = new SystemD();    
    // 系统A独有的数据    
    private String userId = "Java3y";    
    public void doSomething() {      
        // 已经不再需要系统B的依赖了       
        //systemB.SystemBNeed2do(userId);      
        // 系统C和系统D都需要拿着系统A的userId去操作其他的事          			   systemC.SystemCNeed2do(userId);    
        systemD.SystemDNeed2do(userId);   
    } 
} 

```

时间飞逝：

- 又过了几天，系统E的负责人过来了，告诉系统A，需要userId。
- 又过了几天，系统B的负责人过来了，告诉系统A，还是重新掉那个接口吧。
- 又过了几天，系统F的负责人过来了，告诉系统A，需要userId。
- ……

于是系统A的负责人，每天都被这给骚扰着，改来改去，改来改去…….

还有另外一个问题，调用系统C的时候，如果系统C挂了，系统A还得想办法处理。如果调用系统D时，由于网络延迟，请求超时了，那系统A是反馈fail还是重试？？

***，系统A的负责人，觉得隔一段时间就改来改去，没意思，于是就跑路了。

然后，公司招来一个大佬，大佬经过几天熟悉，上来就说：将系统A的userId写到消息队列中，这样系统A就不用经常改动了。为什么呢？下面我们来一起看看：

[![img](../media/pictures/Microservice.assets/1657e6a177e2aa8f6223ea9544523ac5.jpg)](https://s4.51cto.com/oss/201904/15/1657e6a177e2aa8f6223ea9544523ac5.jpg)

系统A将userId写到消息队列中，系统C和系统D从消息队列中拿数据。这样有什么好处？

- 系统A只负责把数据写到队列中，谁想要或不想要这个数据(消息)，系统A一点都不关心。
- 即便现在系统D不想要userId这个数据了，系统B又突然想要userId这个数据了，都跟系统A无关，系统A一点代码都不用改。
- 系统D拿userId不再经过系统A，而是从消息队列里边拿。系统D即便挂了或者请求超时，都跟系统A无关，只跟消息队列有关。

这样一来，系统A与系统B、C、D都解耦了。

**2.2 异步**

我们再来看看下面这种情况：系统A还是直接调用系统B、C、D

[![img](../media/pictures/Microservice.assets/d3580ccb52fa2d96b5492abec9425326.jpg)](https://s2.51cto.com/oss/201904/15/d3580ccb52fa2d96b5492abec9425326.jpg)

代码如下：

```java
public class SystemA {   
        SystemB systemB = new SystemB();  
        SystemC systemC = new SystemC();   
        SystemD systemD = new SystemD();   
        // 系统A独有的数据    
        private String userId ;  
        public void doOrder() {   
        // 下订单         
        userId = this.order();      
        // 如果下单成功，则安排其他系统做一些事     
        systemB.SystemBNeed2do(userId);     
        systemC.SystemCNeed2do(userId);    
		systemD.SystemDNeed2do(userId);    
	} 
} 

```

假设系统A运算出userId具体的值需要50ms，调用系统B的接口需要300ms，调用系统C的接口需要300ms，调用系统D的接口需要300ms。那么这次请求就需要50+300+300+300=950ms

并且我们得知，系统A做的是主要的业务，而系统B、C、D是非主要的业务。比如系统A处理的是订单下单，而系统B是订单下单成功了，那发送一条短信告诉具体的用户此订单已成功，而系统C和系统D也是处理一些小事而已。

那么此时，为了提高用户体验和吞吐量，其实可以异步地调用系统B、C、D的接口。所以，我们可以弄成是这样的：

[![img](../media/pictures/Microservice.assets/30d3012247c59f9a98e6b6277a921f9e.jpg)](https://s2.51cto.com/oss/201904/15/30d3012247c59f9a98e6b6277a921f9e.jpg)

系统A执行完了以后，将userId写到消息队列中，然后就直接返回了(至于其他的操作，则异步处理)。

- 本来整个请求需要用950ms(同步)
- 现在将调用其他系统接口异步化，从请求到返回只需要100ms(异步)

(例子可能举得不太好，但我觉得说明到点子上就行了，见谅。)

**2.3削峰/限流**

我们再来一个场景，现在我们每个月要搞一次大促，大促期间的并发可能会很高的，比如每秒3000个请求。假设我们现在有两台机器处理请求，并且每台机器只能每次处理1000个请求。

[![img](../media/pictures/Microservice.assets/0c376fa4516d99066821976ec70f34e7.jpg)](https://s3.51cto.com/oss/201904/15/0c376fa4516d99066821976ec70f34e7.jpg)

那多出来的1000个请求，可能就把我们整个系统给搞崩了…所以，有一种办法，我们可以写到消息队列中：

[![img](../media/pictures/Microservice.assets/6b9040fb486350734e162c9cf52e1c5a.jpg)](https://s2.51cto.com/oss/201904/15/6b9040fb486350734e162c9cf52e1c5a.jpg)

系统B和系统C根据自己的能够处理的请求数去消息队列中拿数据，这样即便有每秒有8000个请求，那只是把请求放在消息队列中，去拿消息队列的消息由系统自己去控制，这样就不会把整个系统给搞崩。

## **三、使用消息队列有什么问题？**

经过我们上面的场景，我们已经可以发现，消息队列能做的事其实还是蛮多的。

说到这里，我们先回到文章的开头，"明明  JDK已经有不少的队列实现了，我们还需要消息队列中间件呢？"其实很简单，JDK实现的队列种类虽然有很多种，但是都是简单的内存队列。为什么我说JDK是简单的内存队列呢？下面我们来看看要实现消息队列(中间件)可能要考虑什么问题。

**3.1高可用**

无论是我们使用消息队列来做解耦、异步还是削峰，消息队列肯定不能是单机的。试着想一下，如果是单机的消息队列，万一这台机器挂了，那我们整个系统几乎就是不可用了。

[![img](../media/pictures/Microservice.assets/7be3dad31d267e3dd98963e9b9d676fb.jpg)](https://s1.51cto.com/oss/201904/15/7be3dad31d267e3dd98963e9b9d676fb.jpg)

所以，当我们项目中使用消息队列，都是得集群/分布式的。要做集群/分布式就必然希望该消息队列能够提供现成的支持，而不是自己写代码手动去实现。

**3.2 数据丢失问题**

我们将数据写到消息队列上，系统B和C还没来得及取消息队列的数据，就挂掉了。如果没有做任何的措施，我们的数据就丢了。

[![img](../media/pictures/Microservice.assets/83ac129c760ecfc4c09728e99e1f7e32.jpg)](https://s3.51cto.com/oss/201904/15/83ac129c760ecfc4c09728e99e1f7e32.jpg)

学过Redis的都知道，Redis可以将数据持久化磁盘上，万一Redis挂了，还能从磁盘从将数据恢复过来。同样地，消息队列中的数据也需要存在别的地方，这样才尽可能减少数据的丢失。

那存在哪呢？

- 磁盘？
- 数据库？
- Redis？
- 分布式文件系统？

同步存储还是异步存储？

**3.3消费者怎么得到消息队列的数据？**

消费者怎么从消息队列里边得到数据？有两种办法：

- 生产者将数据放到消息队列中，消息队列有数据了，主动叫消费者去拿(俗称push)
- 消费者不断去轮训消息队列，看看有没有新的数据，如果有就消费(俗称pull)

**3.4其他**

除了这些，我们在使用的时候还得考虑各种的问题：

- 消息重复消费了怎么办啊？
- 我想保证消息是绝对有顺序的怎么做？
- ……..

虽然消息队列给我们带来了那么多的好处，但同时我们发现引入消息队列也会提高系统的复杂性。市面上现在已经有不少消息队列轮子了，每种消息队列都有自己的特点，选取哪种MQ还得好好斟酌。

***\****

本文主要讲解了什么是消息队列，消息队列可以为我们带来什么好处，以及一个消息队列可能会涉及到哪些问题。希望给大家带来一定的帮助。

# 13.秒杀交易优化篇（一）消息队列 RocketMQ

## 章节目标

### 掌握缓存库存模型

### 掌握RocketMQ

> 为什么要使用rocketMQ？对比其他消息队列有什么优势？

> 原理：如何运行?

> 安装：如何安装？

> 使用：如何在项目中使用？

## 掌握消息型事务

> 为什么要使用分布式事务？

> 什么叫分布式事务？

> 分布式事务的原理？

> 分布式事务可以分为哪些?

如何使用rocketMQ来保证一致性?

## 缓存库存模型

### 秒杀基础模型

![](../media/pictures/Microservice.assets/fd98c139e1b034a37366314752e503b8.png)

> 在数据库中同步扣减库存这种做法并不高效，满足不了秒杀活动高并发的需求

> 如何改进？

### 改进方案

> 把库存数量存入redis中，扣减库存从redis中去扣减

> 缺点：

1. 依赖redis服务的稳定性
2. 造成缓存库存和数据库库存不一致的情况

> 如何改进？

1. 提高redis服务的可用性，搭建redis主从备份(单机版、主从、哨兵、集群)
2. 发送异步消息去扣减数据库（开启异步线程）
   1. 秒杀优化模型一

![](../media/pictures/Microservice.assets/d48dff6e208c7f817a3f99697ca72acf.png)

> 如何发送异步消息呢？

> 使用消息中间件RocketMQ

## RocketMQ

### 简介

消息中间件是什么？

> 消息中间件利用高效可靠的消息传递机制进行平台无关的数据交流，并基于数据通信来进行分布式系统的集成。

### rocketMQ的前世今生

![1571467534860](../media/pictures/Microservice.assets/1571467534860.png)

> 参考链接：

> <https://yq.aliyun.com/articles/66129>

### 功能

#### 异步化

> 将一些可以进行异步化的操作通过发送消息来进行异步化

![](../media/pictures/Microservice.assets/ee6673bf21c908a7a5f2f306c7da4932.png)

![](../media/pictures/Microservice.assets/579c7cc10f7eb4e9db724ec6bdbb9cbe.png)

#### 高并发削峰

> 在高并发场景下把请求存入消息队列，利用排队思想降低系统瞬间峰值

![](../media/pictures/Microservice.assets/3def5a665f36bfbac59cd21d4bc7b5ff.png)

![](../media/pictures/Microservice.assets/a505734f12233657141a0857aed3b8bd.png)

### 选型

#### ActiveMQ

> ActiveMQ 是Apache出品，最流行的，能力强劲的开源消息总线。ActiveMQ
> 是一个完全支持JMS1.1和J2EE 1.4规范的 JMS Provider实现。

#### RabbitMQ

> AMQP协议的领导实现，支持多种场景。淘宝的MySQL集群内部有使用它进行通讯，OpenStack开源云平台的通信组件，最先在金融行业得到运用。

#### Kafka

> Apache下的一个子项目
> 。特点：高吞吐，在一台普通的服务器上既可以达到10W/s的吞吐速率；完全的分布式系统。适合处理海量数据。

#### RocketMQ

> 阿里巴巴开源项目，现在已经交给Apache管理。特点，高吞吐，功能强大。

### 对比图

![](../media/pictures/Microservice.assets/2eaec06f27be761912635b4ab233cdbf.png)

### 概念模型 

![](../media/pictures/Microservice.assets/48b9df9fc2109cf22533182e5a4f18ed.jpg)

- Producer:

> 消息生成者，负责消息产生，由业务系统负责产生。

- Consumer:

> 消息消费者，负责消费消费，由后台业务系统负责异步消费。

- Topic：消息的逻辑管理单位。

> 这三者是RocketMq中最最基本的概念。Producer是消息的生产者。Consumer是消息的消费者。消息通过Topic进行传递。Topic存放的是消息的逻辑地址。

> 具体来说是Producer将消息发往具体的Topic。Consumer订阅Topic，主动拉取或被动接受消息

![](../media/pictures/Microservice.assets/49e9fe948558bd871fe823081983779a.jpg)

> 注意：一个Producer可以发送消息给多个topic，一个topic可以接受多个producer的消息

- Broker:

> 消息中转角色，负责存储消息，转发消息，一般也称为server

> 可以理解为一个存放消息的服务，里面可以有多个topic

- MessageQueue：

> 消息的物理管理单位，一个Topic下有多个Queue，默认一个topic创建时会创建四个messageQueue

- ConsumerGroup：

> 具有同样逻辑消费同样消息的consumer，可以归并为一个group

- ProducerGroup：

> 通常具有同样属性的一些producer可以归为同一个group。

> 同样属性是指：发送同样topic的消息

- NameServer

> 注册中心

> 作用：

> 每个broker启动的时候会向namesrv注册

> Producer发送消息的时候根据topic获取路由到broker的信息

> Consumer根据topic到namesrv获取topic的路由到broker的信息

## 部署模型

![](../media/pictures/Microservice.assets/0a8d2bc421529505d5d814dc70f1d139.png)

> 注意：NameServer和Broker之间通过心跳机制来检测

## 使用

### 下载

> 下载地址：官网地址：<http://rocketmq.apache.org/release_notes/release-notes-4.4.0/>

![](../media/pictures/Microservice.assets/e376348de0e6e2469180f654d6abc704.png)

![](../media/pictures/Microservice.assets/43469f5c86f02362b1b255843545d443.png)

### 安装

按照上述步骤，下载，解压

注意事项：

1. rocketMQ 是基于java开发的，所以需要配置相应的jdk环境变量才能运行
2. rocketMQ也需要配置环境变量才可在windows上运行

![](../media/pictures/Microservice.assets/b5602d05607b2d123ba1d4a142aaace7.png)

### 启动

1. 修改配置：进入bin目录

![](../media/pictures/Microservice.assets/b1658e987639199192c3b3b5b6089e7c.png)

> 修改NameServer和Broker配置：（windows）

编辑runbroker.cmd文件，修改如下：

![](../media/pictures/Microservice.assets/1cc01dc03393d19dd9ddcc0ffa6345e1.png)

编辑runserver.cmd文件，修改如上图一样

#### 首先启动注册中心nameserver

，默认启动在9876端口，打开cmd命令窗口，进入bin目录，执行命令：

**start mqnamesrv.cmd**

出现以下日志表示启动成功

![](../media/pictures/Microservice.assets/e2bea1f0d3867fb2b490f0a6c48b4c56.png)



这里如果启动不成功，那么就是上面的修改配置没有保存！

1.启动rocketMQ服务，也就是broker

进入bin目录，执行命令：

**start mqbroker.cmd -n 127.0.0.1:9876 autoCreateTopicEnable=true**

端口这个文件在play.cmd

注意：autoCreateTopicEnable=true这个设置表示开启自动创建topic功能，真实生产环境不建议开启。

出现以下日志表示启动成功

![](../media/pictures/Microservice.assets/51c9e23029d24b22bb4df9cfb8723659.png)



两个都启动成功之后，我们可以确认一下是否都启动成功了，可以输入jps -v命令查看状态（jps命令是查看所有额java进程，rocketMQ是运行在jvm上的，所以可以通过此命令查看，）



输入命令jps -l，可以看启动了那个进程和他的端口！！**



![](../media/pictures/Microservice.assets/8bd8073cb70d012920b469bec6a84351.png)

现在，rocketMQ的（单机）服务已经创建成功啦，大家可以愉快的去编程了\~

说明：如果大家是linux/MacOs系统下安装rocketMQ，则更加简单哦，按照官网的说明步骤操作即可。附上链接：<http://rocketmq.apache.org/docs/quick-start/>

补充：

如果大家写完代码之后抛出以下错误

org.apache.rocketmq.client.exception.MQClientException: No route info of this
topic, xxx

那么表示你的rocketMQ中没有创建这个topic,表示开启autoCreateTopicEnable失效了，这个时候需要手动创建topic，还是进入bin目录，执行命令：

./amdin updateTopic -n localhost:9876 -b localhost:10911 -t topicName

然后重新启动一下程序即可。

### 代码测试

导包：

```xml
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-client</artifactId>
    <version>4.4.0</version>
</dependency>

```

#### 消息生产者

![](../media/pictures/Microservice.assets/13860e763738729072e97b1071779aa3.png)

#### 消息消费者

![](../media/pictures/Microservice.assets/cf988d7818c9abb6435cd641fa5ae916.png)



## Java内存区域分布图！

![1571468073593](../media/pictures/Microservice.assets/1571468073593.png)

## 面试题

原地址：https://github.com/SteveYangSunshine/advanced-java

github上面的星很多！ 互联网 Java 工程师进阶知识完全扫盲：涵盖高并发、分布式、高可用、微服务等领域知识，后端同学必看



**如何保证消息的顺序性？**

## 面试官心理分析

其实这个也是用 MQ 的时候必问的话题，第一看看你了不了解顺序这个事儿？第二看看你有没有办法保证消息是有顺序的？这是生产系统中常见的问题。

## 面试题剖析

我举个例子，我们以前做过一个 mysql `binlog` 同步的系统，压力还是非常大的，日同步数据要达到上亿，就是说数据从一个 mysql 库原封不动地同步到另一个 mysql 库里面去（mysql -> mysql）。常见的一点在于说比如大数据 team，就需要同步一个 mysql 库过来，对公司的业务系统的数据做各种复杂的操作。

你在 mysql 里增删改一条数据，对应出来了增删改 3 条 `binlog` 日志，接着这三条 `binlog` 发送到 MQ 里面，再消费出来依次执行，起码得保证人家是按照顺序来的吧？不然本来是：增加、修改、删除；你楞是换了顺序给执行成删除、修改、增加，不全错了么。

本来这个数据同步过来，应该最后这个数据被删除了；结果你搞错了这个顺序，最后这个数据保留下来了，数据同步就出错了。

先看看顺序会错乱的俩场景：

- **RabbitMQ**：一个 queue，多个 consumer。比如，生产者向 RabbitMQ 里发送了三条数据，顺序依次是 data1/data2/data3，压入的是 RabbitMQ 的一个内存队列。有三个消费者分别从 MQ 中消费这三条数据中的一条，结果消费者2先执行完操作，把 data2 存入数据库，然后是 data1/data3。这不明显乱了。

[![rabbitmq-order-01](../media/pictures/Microservice.assets/rabbitmq-order-01.png)](https://github.com/SteveYangSunshine/advanced-java/blob/master/images/rabbitmq-order-01.png)

- **Kafka**：比如说我们建了一个 topic，有三个 partition。生产者在写的时候，其实可以指定一个 key，比如说我们指定了某个订单 id 作为 key，那么这个订单相关的数据，一定会被分发到同一个 partition 中去，而且这个 partition 中的数据一定是有顺序的。
  消费者从 partition 中取出来数据的时候，也一定是有顺序的。到这里，顺序还是 ok 的，没有错乱。接着，我们在消费者里可能会搞**多个线程来并发处理消息**。因为如果消费者是单线程消费处理，而处理比较耗时的话，比如处理一条消息耗时几十 ms，那么 1 秒钟只能处理几十条消息，这吞吐量太低了。而多个线程并发跑的话，顺序可能就乱掉了。

[![kafka-order-01](../media/pictures/Microservice.assets/kafka-order-01.png)](https://github.com/SteveYangSunshine/advanced-java/blob/master/images/kafka-order-01.png)

### 解决方案

#### RabbitMQ

拆分多个 queue，每个 queue 一个 consumer，就是多一些 queue 而已，确实是麻烦点；或者就一个 queue 但是对应一个 consumer，然后这个 consumer 内部用内存队列做排队，然后分发给底层不同的 worker 来处理。 [![rabbitmq-order-02](../media/pictures/Microservice.assets/rabbitmq-order-02.png)](https://github.com/SteveYangSunshine/advanced-java/blob/master/images/rabbitmq-order-02.png)

#### Kafka

- 一个 topic，一个 partition，一个 consumer，内部单线程消费，单线程吞吐量太低，一般不会用这个。
- 写 N 个内存 queue，具有相同 key 的数据都到同一个内存 queue；然后对于 N 个线程，每个线程分别消费一个内存 queue 即可，这样就能保证顺序性。

[![kafka-order-02](../media/pictures/Microservice.assets/kafka-order-02.png)](https://github.com/SteveYangSunshine/advanced-java/blob/master/images/kafka-order-02.png)

# 14.分布式事务

## 知识回顾

### 实现消息队列异步扣减库存

![](../media/pictures/Microservice.assets/f60228a8a6d4aa2e435fb83a294d2063.tiff)

![1572516840916](../media/pictures/Microservice.assets/1572516840916.png)

首先，添加发布库存到缓存接口

然后，整合rocketMQ到项目中，改造代码

### 问题

这种做法能够应用于企业级应用的开发吗？

哪里有问题呢？ 说说你的看法

该如何改进呢？

采用异步的方式去扣减数据库库存，不能使用Spring的事务控制，在发送消息失败或者是扣减数据库库存失败的情况下不能够保证缓存中的库存和数据库中的库存的一致性。

### 改进方案

使用RocketMQ提供的对分布式事务的支持

## 传统事务回顾

### 事务定义：

是数据库操作的最小工作单元，是作为单个逻辑工作单元执行的一系列操作；这些操作作为一个整体一起向系统提交，要么都执行、要么都不执行

### 传统事务知识点

#### 四个特性（ACID）

> 原子性：事务是数据库的逻辑工作单位，事务中包含的各操作要么都做，要么都不做

> 一致性：事务执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。因此当数据库只包含成功事务提交的结果时，就说数据库处于一致性状态。如果数据库系统运行中发生故障，有些事务尚未完成就被迫中断，这些未完成事务对数据库所做的修改有一部分已写入物理数据库，这时数据库就处于一种不正确的状态，或者说是
> 不一致的状态。

> 隔离性：一个事务的执行不能其它事务干扰。即一个事务内部的操作及使用的数据对其它并发事务是隔离的，并发执行的各个事务之间不能互相干扰。

> 持久性：一个事务一旦提交，它对数据库中的数据的改变就应该是永久性的。接下来的其它操作或故障不应该对其执行结果有任何影响。

#### 事务隔离级别

> 读未提交 (Read
> Uncommitted)：允许脏读，也就是可能读取到其他会话中未提交事务修改的数据

> 读已提交(Read
> Committed)：只能读取到已经提交的数据。Oracle等多数数据库默认都是该级别
> (不重复读)

> 可重复读(Repeated
> Read)：在同一个事务内的查询都是事务开始时刻一致的，InnoDB默认级别。在SQL标准中，该隔离级别消除了不可重复读，但是还存在幻象读，但是innoDB解决了幻读

> 序列化：(Serializable)：完全串行化的读，每次读都需要获得表级共享锁，读写相互都会阻塞

#### 事务的传播行为

> Spring 支持 7 种事务传播行为：

> org.springframework.transaction.annotation. Propagation

![](../media/pictures/Microservice.assets/68acb0e4211459cadd4abf30a67c2a30.png)

> REQUIRED
> 是常用的事务传播行为，如果当前没有事务，就新建一个事务，如果已经存在一个事务中，加入到这个事务中。其它传播行为大家可另查阅。

#### 传统事务引用场景举例

![](../media/pictures/Microservice.assets/57f62f90ad2c4ad04b38a5d4533ec69f.png)

![](../media/pictures/Microservice.assets/20a1bfa32a36fbe387fbefcb0a7948e6.png)

![](../media/pictures/Microservice.assets/5953af491baca68d1f754ceb5afe4693.png)

传统事务控制基础：必须得保证是同一个连接，通过jdbc操作数据源的话保证同一个connection 对象

## 分布式事务

### 问题

在分布式架构下，随着业务量的扩大，我们对业务进行拆分，数据库也会

相应的进行分库分片，因为有着网络的不确定性，那么我们分布式环境下

应该如何保证事务的ACID？

![](../media/pictures/Microservice.assets/5b0b844fceca7e26847a08f07e1998f4.png)

当单个数据库的性能产生瓶颈的时候，我们需要对数据库分库或者是分区，那么这个时候数据库就处于不同的服务器上了，因此基于单个数据库所控制的传统型事务已经不能在适应这种情况了，故我们需要使用分布式事务来管理这种情况

### 理论基础-CAP理论

#### 概念

1998年，加州大学的计算机科学家 Eric Brewer 提出，分布式系统有三个指标。

一致性：Consistency

集群中各个结点的数据总是一致的，因此你可以向任意结点读写数据，并总是能得到相同的数据

可用性：Availability

可用性表示你总是能够访问集群（读/写），即使集群中的某个节点宕机了

分区容忍性：Partition toleranc

容忍集群持续运行，即使他们中存在分区(两个分区中的结点都是好的，只是分区之间不能通信)

结论：分布式环境下，CAP不能同时成立

CAP理论图解：

![](../media/pictures/Microservice.assets/fa7bac94fbd9eb9c21747bf0811fe366.jpg)

#### 模型解释

![](../media/pictures/Microservice.assets/e56667b4b2c4848332fbc16e295d338f.png)

1. 如上图所示，假如DB1和DB2都能够正常被访问，只是他们之间不能够互相通信，也就是他们之间不能够同步数据，这个时候我们容忍集群继续运行，那么我们说服务具有分区容忍性
2. 那么现在在分区容忍性的前提之下：（DB1和DB2不能通信，服务继续运行）

现在向DB1中发送一条X=2的更新请求，Datebase1把X值更新为2，但是需要

去同步到Database2，由于DB1和DB2不能够通行，所以同步会失败

A,假如该条请求返回更新成功，那么会导致DB1和DB2数据不一致的情况出现，违背了一致性

B, 假如该条请求返回更新失败，那么我们认为DB1不可用了，违背了可用性

3，分布式系统在什么时候存在不满足分区容忍性的情况呢？

容忍集群持续运行，即使他们中存在分区(两个分区中的结点都是好的，只是分区之间不能通信)

即P不存在，意思就是集群不能容忍分区的出现，也就是不能容忍两个节点之间不能通信的情况，而分布式环境下两个节点不能通信的情况是不存在的，因为节点之间的通信都是通过网络传输，网络是不“靠谱”的。

### 解决方案探索

#### 刚性事务（强一致性）

定义：遵循ACID原则，强一致性。

代表：二阶段提交（2PC）

二阶段提交协议是协调所有分布式原子事务参与者，并决定提交或取消（回滚）的分布式算法。

![](../media/pictures/Microservice.assets/641a263a94547fd63fad6cf896b91421.png)

引入了事务管理器

1. 预备阶段

> 在请求阶段，协调者将通知事务参与者准备提交或取消事务，然后进入表决过程。  
> 在表决过程中，参与者将告知协调者自己的决策：同意（事务参与者本地作业执行成功）或取消（本地作业执行故障）。

1. 提交阶段

在该阶段，协调者将基于第一个阶段的投票结果进行决策：提交或取消。

> 当且仅当所有的参与者同意提交事务协调者才通知所有的参与者提交事务，否则协调者将通知所有的参与者取消事务。参与者在接收到协调者发来的消息后将执行响应的操作。

存在的问题：

同步阻塞问题：在执行的过程中，所有参与的节点都是事务型阻塞的，当参与者占有公共资源时，其他第三方节点访问公共资源不得不处于阻塞状态

不能解决数据不一致的问题

#### 柔性事务（最终一致性）

1. 定义：

> 遵循BASE理论，最终一致性；与刚性事务不同，柔性事务允许一定时间内，不同节点的数据不一致，但要求最终一致。

##### Base理论

> Basically Avaiable，基本可用

> Soft state：软状态

> Eventually consistent：最终一致性

既然无法做到强一致性，但每个应用都可以根据自身的业务特点，采用适当的方式来使系统达到最终一致性。

##### TCC事务

全称：Try-Confirm-Cancel（可以理解为sql中的Lock、Commit、Rollback）

TCC是服务化的二阶段编程模型：

其 Try、Confirm、Cancel 3 个方法均由业务编码实现：Try
操作作为一阶段，负责资源的检查和预留。Confirm
操作作为二阶段提交操作，执行真正的业务。Cancel 是预留资源的取消。

##### 事务流程

![](../media/pictures/Microservice.assets/28f180a658ec113bc5d83b5ac2be47f3.png)

![](../media/pictures/Microservice.assets/ae3da94124f90a2059e342ab5e5627dd.png)

Try阶段：完成所有的业务检查，预留资源

Confirm阶段：更改状态操作

![](../media/pictures/Microservice.assets/dd3e3c58eb8575568880e5a32e3ee8cb.png)

Cancel阶段：当Try阶段存在服务执行失败时，则进入Cancel阶段

缺点：TCC的Try、Confirm、Cancel操作功能按照具体业务来实现，业务耦合度高，开发成本高

##### 本地消息表

本地消息表这个方案最初是ebay提出的分布式事务完整方案https://queue.acm.org/detail.cfm?id=1394128

![](../media/pictures/Microservice.assets/35deabb722edf8e67fc2fb0c49129816.tiff)

![](../media/pictures/Microservice.assets/b392911c1f843814c82762c1e1650658.png)

##### MQ事务消息

![1571732368906](../media/pictures/Microservice.assets/1571732368906.png)

1. 发送事务型消息，该消息暂时不可被消费
2. 消息队列返回发送消息成功状态
3. 本地事务收到消息发送成功状态，然后开始执行本地事务
   1. 假如本地事务执行成功，MQ消息发送方则会告诉MQServer表示这个消息可以被消费了，MQ会投递这个消息到MQ订阅方
   2. 假如本地事务执行失败，MQ消息发送方则会告诉MQServer需要丢弃之前发送的消息
4. 假如MQServer一直没有收到MQ发送方的消息确认通知，会回查本地事务，查看本地事务是否执行成功，假如本地事务执行成功，那么会发送消息，假如本地事务执行失败，那么会丢弃事务，假如本地事务还在初始态，那么会过一会再来询问
5. 消息在MQ订阅方的消息消费成功由MQ来保证

> **如何保证？（记下来，要考）**

> MQ假如投递消息到MQ订阅方失败了，或者MQ订阅方消费消息失败了，那么MQ会把该消息丢入重试队列中，会重试发送该消息，默认16次，直到消息被消费成功为止

> 假如在16次之后该消息还没有被消费成功，那么MQ会再次把该消息丢入MQ死信队列中，对于死信队列的消息，我们需要手动去干预，让他消费成功（例如从后台管理系统手动（或者是定时任务）把死信队列中的消息拿出来，然后手动去执行操作，执行完成之后把消息从死信队列中删除掉）

1. 代码实现
   1. 构建事务型消息生产者

![](../media/pictures/Microservice.assets/e988e69ff6e6ea446b2c549715e690ad.png)

###### 发送事务型消息

![](../media/pictures/Microservice.assets/df88779b5aa09c7005364c6ae77e4687.png)

###### 设置事务监听回调器

1. 执行本地事务
2. 监听本地事务执行状态，用于提供给消息回查

![](../media/pictures/Microservice.assets/d59884944a2affb49e0bcef836c7bf9c.png)

#### 其他成熟解决方案

##### 阿里GTS

成熟的方案，一站式解决，需要付费

参考链接：<https://helpcdn.aliyun.com/product/48444.html>

##### 基于GTS的免费社区版本，SEATA

参考链接：https://github.com/seata/seata



# 15.限流

## 引言

课程回顾：

高并发三把利器：

缓存：

> 提升系统访问速度，增大系统处理流量

限流：

> 限流的目的是通过对并发访问/请求进行限速，或者对一个时间窗口内的请求进行限速来保护系统，一旦达到限制速率则可以拒绝服务、排队或等待、降级等处理

降级：

> 降级是当服务器压力剧增的情况下，根据当前业务情况及流量对一些服务和页面有策略的降级，以此释放服务器资源以保证核心任务的正常运行

> Hystrix

## 章节目标

> 库存售罄解决方案

> 流量削峰技术（削弱流量最高峰值）

> 防刷限流技术

## 库存售罄问题

> 问题：库存售罄了还是会不断的去初始化库存流水

> 如何改进？

> 如果库存售罄了给库存打上售罄标识

> 在请求来之前先去判断库存是否售罄

代码实现：

## 流量削峰技术

流量削峰技术的由来：

主要还是来自于互联网秒杀抢购等业务场景。例如阿里双十一秒杀，短时间上亿用户的涌入，瞬间流量巨大，比如100万人同事抢购一个商品，而商品的库存是100件，这样真实能购买到商品的人数也就是在100人。从业务上来讲，秒杀活动是希望有很多的人参与进来，也就是抢购之前有更多的人看到商品。但是，在抢购时间到达之后，用户开始真正下单时，我们秒杀服务器的后端是绝对不希望有100w用户来同时下单，发起抢购请求。

因为我们都知道服务器处理资源是有限的，所以在出现流量峰值时，很容易导致服务器宕机，出现用户无法访问的情况。

![](../media/pictures/Microservice.assets/7364615b6fa5c05fca4183100247304c.png)

所以我们需要降低流量的峰值！！！

那么如何降低呢？就好比政府为了解决早晚高峰出行的问题，于是就有了错峰限行的解决方案，本质上其实就是限制一部分流量

那么在互联网抢购业务场景之中，我们就有了流量削峰技术。

解决方案大致

### 秒杀令牌

#### 缺点

> 秒杀下单接口会被脚本不停的刷新

1. 影响正常用户下单的流程
2. 黄牛用户在活动未开始之前也会对秒杀下单接口不停的刷新，无疑对数据库造成的不必要的压力

> 秒杀验证逻辑和秒杀下单接口强关联，代码冗余度高

秒杀下单验证逻辑复杂，对交易接口产生无关联负载

#### 秒杀令牌原理

> 秒杀接口需要依靠令牌才能进入

> 秒杀下单之前用户需要先获得令牌

> 在请求下单接口之前，先去获取一个秒杀令牌，如果获取到了令牌，然后再拿秒杀令牌去请求下单接口

#### 秒杀令牌代码实现

### 秒杀大闸

#### 缺点

> 秒杀令牌只要活动一开始就会无限制生成，影响系统性能

#### 原理

> 依靠秒杀令牌的授权原理定制化发牌逻辑，做到大闸的功能

> 依靠秒杀令牌初始库存颁发对应数量的令牌，控制大闸流量

> 库存售罄判断前置到秒杀令牌发放中

#### 代码实现

### 队列泄洪

#### 秒杀令牌与秒杀大闸控制缺点

1. 浪涌流量涌入后系统无法应对

2. 多库存，多商品等令牌的限制能力比较弱

   #### 原理

> 本质：排队策略

> 排队有时候比并发更加高效（例如Redis单线程模型，innodb的mutex key等）

> Alisql对innodb的优化策略

> 依靠排队去限制并发流量

> 依靠排队和下游拥塞窗口的程度调整队列释放流量的大小

> 举例：支付宝银行网关队列举例 Zqueue

#### 队列泄洪代码实现

#### 本地or分布式

本地：将队列维护在本地内存中

分布式：将队列设置到外部redis内

## 防刷限流技术

### 验证码

### 限流算法

限流目的：

流量远比你想的要多

系统活者总比挂了要好

宁愿只让少数人能用，也不要让所有人都不能用

#### 限流方案

1. 限并发（限制同一时间运行同一个接口的并发数量）
2. 令牌桶算法
3. 漏桶算法
   1. 令牌桶算法

![](../media/pictures/Microservice.assets/ce449de128a024722b5f3b80007663f1.png)

#### 漏桶算法

![](../media/pictures/Microservice.assets/a136691eef3165bab05bc891c51c0754.png)

#### 比较优缺点：

漏桶算法：能否强行限制请求处理的速度

令牌桶算法：除了能够在总体上限制数据的平均传输速率以外，还允许某种程度上的突发传输。在令牌桶的传输中，只要令牌桶中存在令牌，那么就允许突发的数据传输直到用户配置的上限，因此令牌桶更加适用于突发流量。

#### 令牌桶实例

Google提供 的Guava工具包中的RateLimiter

谷歌觉得jdk中的一些工具包,有点low, 自己分装了一些工具包!   

```xml
<dependency>
    <groupId>com.google.guava</groupId>
    <artifactId>guava</artifactId>
    <version>19.0</version>
    <scope>compile</scope>
</dependency>

```



# 16.缓存

## 缓存设计

### 缓存的好处

#### 加速读写

> 缓存基于内存，能够快速响应

#### 降低后端负载

> 减少后端DB操作，降低mysql负载

### 缓存的缺点

#### 数据不一致

> 会造成缓存和数据库不一致的问题

#### 代码维护成本

> 多了一层缓存逻辑

#### 运维成本

> 例如Redis、Memche

### 缓存设计的原则

> 快速存取设备，用内存

> 将缓存尽可能推到离用户最近的地方

> 脏缓存清理（比如说修改了数据库）

## 多级缓存

后端架构图

![](../media/pictures/Microservice.assets/890c7c54943636a5bda8bf72be7d9136.png)

### Redis缓存

### 热点数据本地缓存

#### 特点

1. 热点数据
2. 脏读不敏感
3. 内存可控

本地热点数据的生命周期必定不会很长

#### 解决方案

##### HashMap&ConcurrentHashMap

HashMap缺点：

1. 不支持并发读并发写
2. 线程不安全

线程安全？HashTable

ConcurrentHashMap:

缺点：

不支持缓存时间

不支持热点数据淘汰策略

##### Guava Cache

优点：

1. 线程安全
2. 支持缓存时间设置
3. 支持热点数据失效淘汰机制

代码实现：

![](../media/pictures/Microservice.assets/3288d582a0eff0fca0f934a0e3fa8d6e.png)

LRU：Least recently used 最近最少使用

缓存性能测试

### Nginx缓存

![](../media/pictures/Microservice.assets/10eaa9818e9cff10ca451ed8f49391fe.png)

Levels：对应文件的级别（做二级目录，先将一个文件的url做一次hash，取一位作为第一级文件目录的索引，再取一位作为第二级文件目录的索引）

Keys_zone: 在nginx中开了100m内存大小的空间用来存放Key

Inactive：文件存放周期为7天

Max_Size: 最多存10G的文件，如果超过10个G，那么将采用LRU策略淘汰



这次项目中电影院首页用到缓存技术!

就是将首页需要的数据放到缓存中!然后下一次刷新的时候,不用再次查询数据库!

这样速度会快很多!



### 这里用到的一个注解:@PostConstruct

?????然后查一下!

























