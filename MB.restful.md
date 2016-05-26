title: MB.restful
speaker:  珠峰培训
url: http://www.zhufengpeixun.com
transition: cards
theme: blue
highlightStyle:javascript

[slide]
#8.8 REST
Resources Representational State Transfer(资源表现层状态转化)

* 资源（Resources）网络上的一个*实体*,每种资源对应一个特定的URI  {:&.zoomIn}
* 表现层（Representation） 资源呈现出来的*形式*叫做表现层
* 状态转化（State Transfer）HTTP协议里面，四个表示操作方式的*动词*对应四种基本*操作*
* 某些动作是HTTP`动词`表示不了的，你就应该把动作做成一种资源

[note]
1. 所谓"资源"，就是网络上的一个实体。它可以是一段文本.URI（统一资源定位符）指向它.
2. 文本可以用txt格式表现，也可以用HTML格式,URI只代表资源的实体，形式应用Accept和Content-Type字段指定
3. 访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。
如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）
[/note]

[slide]
#RESTful API设计 
* 使用HTTP`协议`   {:&.zoomIn}
* URL中只有`名词`
* HTTP动词
  * GET 从服务器`获取`资源（一项或多项）  {:&.zoomIn}
  * POST在服务器`新建`一个资源。
  * PUT 在服务器`更新`资源（客户端提供改变后的`完整`资源）。
  * PATCH 在服务器更新资源（客户端提供改变的`属性`）。
  * DELETE 从服务器`删除`资源。
* 查询字符中指定`过滤`条件
  * 当前页   {:&.zoomIn}
  * 每页数量
  * 过滤关键字
  * 排序字段

[slide]
#RESTful API设计   
* GET /collection：返回资源对象的`列表`（数组） {:&.zoomIn}
* GET /collection/id：返回`单个`资源对象
* POST /collection：返回`新生成`的资源对象
* PUT /collection/id：返回`完整`的资源对象
* PATCH /collection/id：返回`完整`的资源对象
* DELETE /collection/id：返回一个`空资源`
  
[slide]
##curl用法
|参数|含义|
|:-----|:-----|
|-H|传头信息 注意 key 和 value 之间使用冒号|
|--data|传递请求体|
|-X|指定方法|

[slide]
##curl示例
* 查询所有的用户 curl -v -H 'accept:text/html'  http://localhost:8080/users
* 查询指定的用户 curl -v -H 'accept:text/html'  http://localhost:8080/users/1
* 添加用户 curl -v -X POST --data "name=zfpx300&age=300"  http://localhost:8080/users
* 修改用户(参数为完整的属性) curl -v -X PUT --data "id=1&name=zfpx120&age=120"  http://localhost:8080/users/1
* 修改用户(参数为变更的属性) curl -v -X PATCH --data "age=120"  http://localhost:8080/users/1
* 删除用户 curl -v -X DELETE --data "id=1"  http://localhost:8080/users
* 过滤条件 http://localhost:8080/users?pageNum=1&pageSize=2&keyword=&sortBy=age

[note]
http://www.ruanyifeng.com/blog/2011/09/restful.html
http://www.ruanyifeng.com/blog/2014/05/restful_api.html
http://loopback.io/getting-started/
[/note]
