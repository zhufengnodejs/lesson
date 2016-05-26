title: MD.express应用
speaker: 珠峰培训
url: https://github.com/zhufengpeixun
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: blue
usemathjax: yes

[slide]
#多语言
可以通过请求头判断客户端期望的语言版本
* 请求头 `Accept-Language:en,zh-CN;q=0.8,zh;q=0.6`
* 响应头 `Content-Language: en`

[slide]
#客户端检测
* User Agent中文名为`用户代理`，是Http协议中的一部分
* 是一种向访问网站提供你所使用的浏览器类型及版本、操作系统及版本、浏览器内核、等信息的标识
* 通过这个标识，用户所访问的网站可以显示`不同的排版`从而为用户提供更好的体验或者进行`信息统计`
* 识别是否为手机客户端的只要识别`User-Agent`中是否有 `"Mobile"` 字段即可
* `user-agent-parser`模块可以解析用户代理

[slide]
#多个域名共用80端口
* 虚拟主机是把一台真实的物理电脑主机分割成多个单元，每个单元都具有`单独域名`和`相同的端口`。
* 代理一般分为正向代理和反向代理。
  * 正向代理的典型用途是为在防火墙内的局域网客户端提供访问Internet的途径
  * 反向代理的典型用途是将防火墙后面的服务器提供给Internet用户访问
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/proxy.png" class="img-responsive"> 

[slide]
#缓存作用
* 减少了冗余的`数据传输`，节省了网费。
* 减少了服务器的负担， 大大提高了网站的`性能`
* 加快了客户端加载网页的`速度`

[slide]
#请求流程
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/cachestart.png" class="img-responsive">
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/cachecontrol.png" class="img-responsive"> 


[slide]
#通过最后修改时间来判断缓存是否可用
1. Last-Modified：响应时告诉客户端此资源的`最后修改时间`
2. `If-Modified-Since`：当资源过期时（使用Cache-Control标识的max-age），发现资源具有*Last-Modified*声明，则再次向服务器请求时带上头*If-Modified-Since*。
3. 服务器收到请求后发现有头*If-Modified-Since*则与被请求资源的最后修改时间进行比对。若最后修改时间较新，说明资源又被改动过，则`响应最新的资源`内容并返回200状态码；
4. 若最后修改时间和*If-Modified-Since*一样，说明资源没有修改，则响应304表示`未更新`，告知浏览器继续使用所保存的缓存文件。


[slide]
#最后修改时间存在问题
1. 某些服务器不能精确得到文件的`最后修改时间`， 这样就无法通过最后修改时间来判断文件是否更新了。
2. 某些文件的修改非常频繁，在秒以下的时间内进行修改. Last-Modified只能`精确到秒`。
3. 一些文件的最后修改时间改变了，但是`内容并未改变`。 我们不希望客户端认为这个文件修改了。
4. 如果同样的一个文件位于多个`CDN`服务器上的时候内容虽然一样，修改时间不一样。

[slide]
#ETag
ETag是实体标签的缩写，根据实体内容生成的一段`hash`字符串,可以标识资源的状态。当资源发生改变时，ETag也随之发生变化。
ETag是Web服务端产生的，然后发给浏览器客户端。
1. 客户端想判断缓存是否可用可以先获取缓存中文档的*ETag*，然后通过*If-None-Match*发送请求给Web服务器询问此缓存是否可用。
2. 服务器收到请求，将服务器的中此文件的*ETag*,跟请求头中的*If-None-Match*相比较,如果值是一样的,说明缓存还是最新的,Web服务器将发送*304 Not Modified*响应码给客户端表示缓存未修改过，可以使用。
3. 如果不一样则Web服务器将发送该文档的最新版本给浏览器客户端


[slide]
#如何干脆不发请求
浏览器会将文件缓存到Cache目录，第二次请求时浏览器会先检查Cache目录下是否含有该文件，如果有，并且还没到**Expires**设置的时间，即文件还没有过期，那么此时浏览器将直接从**Cache**目录中读取文件，而不再发送请求
* **Expires**是服务器响应消息头字段，在响应*http*请求时告诉浏览器在过期时间前浏览器可以直接从浏览器缓存取数据，而无需再次请求
* **Cache-Control**与**Expires**的作用一致，都是指明当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据,如果同时设置的话，其优先级高于**Expires**

[slide]
##请求头
|头信息|含义|
|:------|:------|
|Cache-Control: max-age=0|Cache -Control指定请求和响应遵循的缓存机制,以秒为单位,表示不缓存|
|If-Modified-Since: Mon, 19 Nov 2012 08:38:01 GMT|缓存文件的最后修改时间|
|If-None-Match: "0693f67a67cc1:0"|缓存文件的Etag值|
|Cache-Control: no-cache|不使用缓存|

##响应头
|头信息|含义|
|:------|:------|
|Expires: Mon, 19 Nov 2012 08:40:01 GMT|缓存过期的时间（绝对时间）|
|Cache-Control: max-age=60|60秒之后缓存过期（相对时间）|
|ETag: "20b1add7ec1cd1:0"|	服务器端文件的Etag值|
|Last-Modified: Mon, 19 Nov 2012 08:38:01 GMT|服务器端文件的最后修改时间|


[note]
HTTP请求中浏览器的缓存机制 http://kb.cnblogs.com/page/73901/
浏览器 HTTP 协议缓存机制详解 http://my.oschina.net/leejun2005/blog/369148
HTTP协议 (四) 缓存 http://www.cnblogs.com/TankXiao/archive/2012/11/28/2793365.html 
[/note]










