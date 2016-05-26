title: QD.爬虫
speaker:  珠峰培训
url: http://www.zhufengpeixun.com
transition: cards
theme: blue
highlightStyle:javascript

[slide]
#网络爬虫
网络爬虫是一种自动*获取网页内容*的程序,功能如下
* 发出HTTP请求获取指定URL中的内容 {:&.moveIn}
* 使用`jQuery`的语法操作网页元素，提取需要的元素
* 将数据保存到`mysql`数据库中
* 建立web服务器*显示*这些数据
* 使用计划任务*自动执行*更新任务
* 布署项目到*阿里云*中并配置*反向代理*

[slide]
#async
async是一个*流程控制库*,为我们带来了丰富的嵌套解决方案。
https://www.npmjs.com/package/async

[slide]
#request
一个简单的HTTP请求工具,用来*获取网页*内容
https://www.npmjs.com/package/request

[slide]
#cheerio
在服务器端实现了`jQuery`中的DOM操作API
https://www.npmjs.com/package/cheerio

[slide]
#cron
用来周期性的执行某种任务或等待处理某些事件的一个守护进程
https://www.npmjs.com/package/cron
<img src="http://images.cnitblog.com/blog/34483/201301/08090352-4e0aa3fe4f404b3491df384758229be1.png" class="img-responsive">

* 星号（*）：代表所有*可能*的值
* 逗号（,）：可以用逗号隔开的值指定一个*列表范围*，例如，“1,2,5,7,8,9”
* 中杠（-）：可以用整数之间的中杠表示一个*整数范围*，例如“2-6”表示“2,3,4,5,6”
* 正斜线（/）：可以用正斜线*指定时间*的*间隔频率*，*/10，如果用在minute字段，表示每十分钟执行一次

[slide]
#debug
根据环境变量的有选择向控制台输出调试信息
https://www.npmjs.com/package/debug

[slide]
#child_process
此内置模块用于启动一个新的`子进程`




 

