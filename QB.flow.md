title: QB.异步编程
speaker:  珠峰培训
url: http://www.zhufengpeixun.com
transition: cards
theme: blue
highlightStyle:javascript

[slide]
#为什么要使用异步编程
* *异步*就是一个任务不连续执行 {:&.zoomIn}
* *同步*就是一个任务连接执行完
* 异步编程可以在单线程的情况下提高*并发*

[note]
比如，有一个任务是读取文件进行处理，任务的第一段是向操作系统发出请求，要求读取文件。然后，程序执行其他任务，等到操作系统返回文件，再接着执行任务的第二段（处理文件）。这种不连续的执行，就叫做异步。
相应地，连续的执行就叫做同步。由于是连续执行，不能插入其他任务，所以操作系统从硬盘读取文件的这段时间，程序只能干等着。
[/note]

[slide]
#异步编程时如何实现流程控制
* *回调*函数callbacks {:&.zoomIn}
* *事件*机制
* *Promise *

[slide]
#回调函数callbacks
<pre><code class="javascript">
fs.readFile('1.txt','utf8',function(err,data){
   fs.readFile(data,'utf8',function(err,data2){
       console.log(data2);
   });
})
</code></pre>

[slide]
##事件
```
var EventEmitter  = require('events');
var events = new EventEmitter();

events.on('done',function(filename){
    task2(filename);
});
```

[slide]
##Promise
* Promise表示一个*异步*操作的最终*结果*。
* Promise最主要的交互方法是通过将函数传入它的`then`方法从而获取得Promise最终的*值*或Promise最终最*拒绝*（reject）的*原因*。
* promise状态由*内部*控制，*外部*不可变
* 状态只能从`pending`到`resovled`, `rejected`，一旦进行完成不可逆
<img src="https://camo.githubusercontent.com/936320d9d13426d9631ff49d817b5d542e135d10/687474703a2f2f7777772e616c6c6f797465616d2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031352f30352f515125453625383825414125453525394225424532303135303533303230313332382e706e67" class="img-responsive">


[slide]
##async
* series 串行执行 {:&.zoomIn}
* waterfall 瀑布模式
* parallel 并行执行
* auto 串并混合



