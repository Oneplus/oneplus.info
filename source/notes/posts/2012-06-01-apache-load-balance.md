---
layout: note
title: "Apache负载均衡"
author: Oneplus
tags:
 - Server
---

Apache也是可以实现负载均衡的。Apache的负载均衡主要是通过`mod_proxy_balancer`实现的。那么，apache负载均衡的配置方法是什么样的？

在apache的配置文件`httpd.conf`中加入

~~~bash
ProxyPass / balancer://proxy/         #注意这里以"/"结尾 
<Proxy balancer://proxy> 
    BalancerMember http://192.168.6.37:6888/ 
    BalancerMember http://192.168.6.38:6888/ 
</Proxy> 
~~~

这里不一定要在`httpd.conf`中直接添加`ProxyPass / balancer`。另一种实现方法是向`httpd.conf`中添加`Include conf/httpd-proxy.conf`，然后把`ProxyPass`写到`httpd-proxy.conf`中。

下面详细介绍这段配置文件的含义：
  
* 其中`ProxyPass`是配置虚拟服务器命令
* /应该是类于过滤规则，指的是web请求url的后缀（参考网址中说是前缀，不懂）。如果只对`/redmine`的请求进行负载均衡，那么需要改成`/redmine`。
* `balancer://proxy`表示要配置负载均衡，`proxy`表示负载均衡名，也可以改成其他名字，比如说`redmine_cluster`。

~~~bash
BalancerMember http://192.168.6.37:6888/ 
~~~

表示将`http://192.168.6.37:6888/`注册到负载均衡中。

上述所示的负载均衡是轮询型负载均衡，除此之外，还有按权重分配负载均衡策略，权重请求响应负载均衡策略。其中，前者按照请求次数分配负载，后者则按照请求负载分配负载。举个例子讲：按照前者，如果有4次请求，3次被分配到机器A、1次被分配到机器B。按照后者，有1000bytes的请求，750bytes被分配给A、250bytes被分配给B。具体参考下面的链接

#### 参考

* [apache2.2.4 负载均衡初探](http://blog.csdn.net/paulluo0739/article/details/2269052)
