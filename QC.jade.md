title: QC.jade
speaker:  珠峰培训
url: http://www.zhufengpeixun.com
transition: cards
theme: blue
highlightStyle:javascript

[slide]
#jade模板
Jade是一款高性能简洁易懂的模板引擎.

[slide]
##jade安装
* jade转html http://jade-lang.com
* html转jade  http://www.html2jade.org/

```
npm install jade -g
jade -h
```


[slide]
##文档声明和头尾标签
```
doctype html
html
   head
      title zfpxnode.js
   body
```

[slide]
##命令行实时编译
* 可以通过命令行进行编译 `jade index.jade`
* -P 表示有美化缩进 `jade  -P index.jade`
* -w 有变化，实时监控 `jade  -P -w index.jade`

[slide]
##标签语法
```
doctype html
html
   head
      title zfpxnode.js
   body
      h1 welcome to zfpx to study node.js
```

[slide]
#属性文本和值

```
#id.classname(title="hello") zfpx
```

[slide]
#混合的成段文本和标签
多行换行的文本,有两种，一种是前面加 |,一种是标签后面加.
```
      p
         | 1.a
      p.
         1. a
```

[slide]
#循环
```
  - var courses = ['node.js','jade']
    each item in courses
      p=item
  - for(var i=0;i<3;i++){
    p=i
  -}    
```

[slide]
#判断
```
- var name = 'zfpx'
if name == 'zfpx'
else
  p I don't know you
```

[slide]
#模板之间的继承
1. 模板的继承,通过`block extends`实现。块看做`block`,实现递归。
2. `block`可以定义，可以多次调用
3. 子文档里可以覆盖父文档里的东西

[slide]
#模板之间的包含
1. 模板的包含解决的是文件和文件之间的*包含*关系
2. include可以包含一段HTML代码，CSS样式
3. include的时候如果加了`文件扩展名`，就会`直接`包含，而不是用`jade`编译。
