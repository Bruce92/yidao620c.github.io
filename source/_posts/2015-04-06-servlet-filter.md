---
layout: post
title: "servlet filter详解"
date: 2015-04-06 21:08:25 +0800
comments: true
categories: Web开发
---

在写一个springmvc项目中想对用户的请求进行拦截，只有登录用户才能访问资源。这时候可以使用到SpringMVC的拦截器Intercepter，但是这个只能局限在SpringMVC中使用，如果想更加通用一点，最好使用Servlet Filter实现这个需求。

本文将通过几个实际的例子展示下Servlet中的Filter的使用。

1). 我们为什么需要使用Filter？

通常我们会使用session来保存登录用户的信息，通过从session中取出保存的属性值来判断用户是否登录，但是如果我们有大量的请求方法，每个人方法中都这样去判断就会有很多重复代码，将来我们想改动下逻辑，那得改动所有的请求方法实现，所以这个是不可取的。

这时候就是使用Servlet Filter的时候了，它是可插拔的，对于普通的action方法来讲是透明的。它会在执行其他方法之前或将结果返回给客户端之前来执行其他逻辑。

以下几种场景下我们会使用到Servlet Filter：

- 将请求的参数写入日志文件
- 对于资源的访问进行统一的授权与验证
- 在请求到达实际Servlet之前格式化请求内容或请求头
- 压缩返回数据后发送给客户端
- 修改返回内容，增加一些cookie、header等信息<!--more-->

前面提到过，Servlet是可插拔的，可以通过在web.xml中配置是否使用。如果我们定义了多个Filter，就会形成一个过滤器链。
通过实现接口javax.servlet.Filter来创建一个过过滤器。

2).  Filter接口

Filter接口包含了三个跟生命周期有关的方法，并且由Servlet容器来管理。它们分别是：