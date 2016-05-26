title: LH. 前后端分离
speaker: 珠峰培训
url: https://github.com/zhufengpeixun
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: blue
usemathjax: yes

[slide]
#什么是前后端分离
* 前端：负责`View`和`Controller`层。
* 后端：只负责`Model`层，业务和数据处理等。

[slide]
#为什么要前后端分离？
* *后端*为主的MVC,遇到同步异步结合的页面沟通麻烦
* Ajax为主*SPA*型开发模式, 如果一个页面请求过多则性能较低
* 前后端职责不清
* 限制了前端的发挥空间

[note]
1. 在业务逻辑复杂的系统里，我们最怕维护前后端混杂在一起的代码，因为没有约束，M-V-C每一层都可能出现别的层的代码
2. 对前端发挥的局限 Comet、Bigpipe
3. 如果前端掌握了Controller，我们可以做url design，我们可以根据场景决定在服务端同步渲染，
还是根据view层数据输出json数据，我们还可以根据表现层需求很容易的做Bigpipe,Comet,Socket等等，完全是需求决定使用方式。
[/note]

[slide]
#基于Node.js的前后端分离
* 后端提供API数据接口
* 前端负责渲染模板和页面

[slide]
#案例
* 抓取百度百家生成新闻列表
```
response.on('end',function(){
            var reg = /<a href=".*" target="_blank" mon="col=\d+&pn=\d+">(.*)<\/a>/g;
            var matched = result.match(reg);
            var ret = [];
            for(var i = 0; i < matched.length; i++){
               ret.push({a:matched[i]});
            }
            res.end(JSON.stringify(ret));
         });
```
















