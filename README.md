# micro_trade
由SpringBoot+vue制作的交易平台

### 前言

本人做了一个交易平台，后端是SpringBoot，前端是Vue。这个电商平台有分**商家页面**和**普通用户页面**，后续还会增加一个独属于**管理员的页面**。这个电商平台通过**QQ登录进行注册**，并且为每一个注册的的用户分配一个默认好友，可以进行聊天，每一个普通的用户都可以通过申请提交成为一名商家，成为商家之后才可以进行增加自家的商品。

其实本人之前也做过一个前后的耦合的thymeleaf和SpringBoot的商城，后续也曾想过下一个项目是不是该做一个博客，音乐平台，或者是视频网站，最后考虑到，用工具的方法有千千万万，重要的是对工具的了解程度如何，你能不能更加深入的对单个方面有较为深刻的理解，于是这个项目也是一个电商平台，但在实现了前后端分离的同时，还加入了很多新的技术，并且在一些方面有了更为优秀的解决方案。

### 特点

看文章有时候就和看别人家的注释一样，不一定能快速分清楚对方的注释是关键语句还是在水代码行数，所以前面先列出本人做的项目的特点，节约一下阅读的时间，后面会有较为详细的描述。

**实现的模板**：基本CRUD和购物车，秒杀商品，搜索，Socket通信，security安全拦截，微服务等。

**一些特点**：

- 使用了redis，在用户访问商品时候会把商品放入redis缓存器，减少数据库的频繁访问，并且使用redis集群实现数据的安全
- 使用了redis实现了商品的秒杀，对突然间大量的请求会将其放入redis而不放入数据库，等秒杀活动过了一定时间再使用定时任务，慢慢写入数据库，由于redis的单线程保证了秒杀的安全，也减少了数据库的访问压力，后续的云服务还可以通过将商品放入消息队列的方式，进一步提高性能。
- 图片的类型是String，而不是流文件，这里结合了七牛云做图床，实现图片数据库和本地数据库的分离
- 每一个用户会有一个默认的好友，以用来测试socket模块，socket模块实现了用户的实时在线聊天，并且还会保存用户的聊天信息。
- 申请了QQ互联的功能，只需要QQ扫码便可以进行登录，QQ互联是和VUE 进行结合的，会产生一个全局的JWT来保证用户的权限认证，后端的security也是用JWT来和前端进行权限认证
- 搜索模块结合了Elasticsearch，以便于用户进行模糊类型的搜索
- 商品平台里面的数据是使用Jsoup爬虫从京东爬取而来的，并且使用雪花算法为每一个商品生成了一个全局唯一的UID
- 结合eureka和ribbon实现注册中心和负载均衡，降低访问压力





## 项目讲述

### 所用技术

1. SpringBoot （后端）
2. MySQL （数据库）
3. MyBatis （访问数据库）
4. swagger （集成文档）
5. SpringSecurity （登录与权限控制）
6. JWT （单点登录）
7. Jsoup （爬虫，用于补充数据库的数据）
8. fastjson （转JSON工具，用于前后端数据交互）
9. 七牛云 （图床）（已废除）
10. netty-socketio （用于用户之间的通信）
11. qq互联 （实现QQ登录）
12. redis （中间件，用于数据的缓存）
13. elasticsearch （搜索引擎）
14. spring-boot-admin （管理后台）
15. eureka （微服务的注册中心）
16. ribbon （负载均衡）
17. docker （容器化）
18. Nginx （反向代理）
19. aliyunEcs （服务器）
20. vue （前端）
21. axios （前端api） 
22. Element-ui （前端UI）

后续写在了：https://pandalee99.github.io/