## Nacos的下载与部署

去github上拉取nacos

https://github.com/alibaba/nacos/tags

![image-20220621084202817](nacos.assets/image-20220621084202817.png)

就是一个绿色版的压缩包

![image-20220621084231415](nacos.assets/image-20220621084231415.png)

二选一安装即可

![image-20220621084343840](nacos.assets/image-20220621084343840.png)

解压变成

![image-20220621084425431](nacos.assets/image-20220621084425431.png)

进入bin启动cmd

startup.cmd -m standalone shutdown.cmd 

![image-20220621084633955](nacos.assets/image-20220621084633955.png)



访问地址

http://localhost:8848/nacos/

![image-20220621084831097](nacos.assets/image-20220621084831097.png)

内部页面

![image-20220621084917897](nacos.assets/image-20220621084917897.png)

以上是部署在windows系统上,一般可以运行在Linux系统中



## 代码层面的配置

这里建**两个独立的微服务**

![image-20220621163605886](nacos.assets/image-20220621163605886.png)

order是订单模块,其service层会用RestTemplate去向user用户模块发http请求(便于后续观察负载均衡)

![image-20220621163809825](nacos.assets/image-20220621163809825.png)

引入springcloudalibaba的父工程依赖

```
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.2.6.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

在各个子微服务(**user-service**和**order-service**)中引入nacos-discovery依赖(服务发现)

```
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

然后需要在各个子工程中的application.yml,加入nacos的地址,这一步告诉本地的服务,去哪注册nacos

```
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
```

这一步一写,只要服务启动,在nacos上就能看见服务,便于运维(服务一起,就可以在不动代码的情况下,进行服务的运维)

![image-20220621164919641](nacos.assets/image-20220621164919641.png)

## 集群配置

并非是高大上的操作

就是我们一份服务代码,可以被复制成多份,部署在不同的服务器上,当然出于容灾考虑,大公司的服务器分布在不同的省份和地区

那么我们可以将一部分服务器上的相同服务代码,划分为一个集群.

集群为的是,提高服务的并发量,维持服务的高可用性

![image-20220621165553137](nacos.assets/image-20220621165553137.png)



代码层面只要修改yml即可

```
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ # 集群名称
```

order的配置

![image-20220621170045296](nacos.assets/image-20220621170045296.png)

user的配置

![image-20220621170130670](nacos.assets/image-20220621170130670.png)



同是一个集群的微服务,优先进行负载均衡,比如这俩都是HZ集群

 可以在idea中复制几个User的微服务,**改一下端口号**,防止冲突,**改一下集群**,看看负载均衡效果

```
-Dserver.port=8083 -Dspring.cloud.nacos.discovery.cluster-name=SH
```

![image-20220621170921960](nacos.assets/image-20220621170921960.png)



这里有一个order是HZ集群,三个user,两个是HZ集群,一个是SH集群

![image-20220621171210495](nacos.assets/image-20220621171210495.png)

同一集群内,还可以通过群众配置,调整负载均衡的概率

![image-20220621171403333](nacos.assets/image-20220621171403333.png)

 

负载均衡测试

postman发10次请求

![image-20220621171446346](nacos.assets/image-20220621171446346.png)

同集群优先处理,但多次高频点击,其它集群也可能收到,然后是权重,权重比例与负载均衡概率相当.

权重为0,则不接受任何负载均衡, 有利于版本更新时的操作



## 环境隔离

可以做到生产的服务归生产,开发的归开发,测试的归测试

![image-20220621172052203](nacos.assets/image-20220621172052203.png)



![image-20220621172148303](nacos.assets/image-20220621172148303.png)

将命名空间id复制到配置文件

![image-20220621172250268](nacos.assets/image-20220621172250268.png)

配置之后,order绝迹江湖,因为他去了另一个空间

![image-20220621172647461](nacos.assets/image-20220621172647461.png)