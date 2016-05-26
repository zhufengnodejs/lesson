title: OB. Angular.js
speaker:  珠峰培训
url: http://www.zhufengpeixun.com
transition: cards
theme: blue
highlightStyle:javascript

[slide]
##为什么要学习Angular.js
1. 面试要问 {:&.rollIn}
2. 现在使用<span class="text-danger">最广泛</span>的框架之一
3. <span class="text-danger">前后端分离</span>，后端只提供<span class="text-danger">数据接口</span>，<span class="text-danger">路由和模板渲染</span>等都在前端完成
4. html和js分离,<span class="text-danger">展示</span>和<span class="text-danger">逻辑</span>分离
5. 减少JS代码,减少DOM元素查找，事件绑定等代码
6. 适合<span class="text-danger">API</span>的方式进行开发

[slide]
##angular使用流程
1. *使用bower下载*angular.js   http://school.zhufengpeixun.cn/course/40 {:&.rollIn}
2. <span class="text-danger">引入</span>angular.js脚本文件到当前页面
3. 通过指定`ng-app`定义angular应用的<span class="text-danger">控制范围</span>
4. 一切从模块开始，先<span class="text-danger">定义模块</span>
5. 在模块下声明<span class="text-danger">控制器</span>,注入`$scope`并进行初始化
6. 在<span class="text-danger">DOM元素</span>上通过`ng-controller`指定此控制器
7. 在此DOM元素下面编写<span class="text-danger">表达式</span>读取`$scope`上的属性值
[note]老项目定义到html上，新项目定义到某一部分上[/note]


[slide]
##ng-app
可以用ng-app 指令告诉Angular 应该管理页面中的哪一块,声明了`ng-app`的元素会成为$rootScope的起点，而$rootScope是作用域链的根,也就是说根下的作用域都可以访问它。
```
<html ng-app="myApp">
<body>
    {{ someProperty }}
</body>
```

[slide]
##ng-model
* 在AngularJS中，只需要使用`ng-model`指令就可以把应用程序<span class="label label-danger">数据</span>绑定到<span class="label label-danger">HTML元素</span>，实现model和view的**双向绑定**。
* `ng-model`把相关处理事件绑定到指定标签上，这样我们就可以不用在手工处理相关事件(比如change等)的条件下完成对数据的展现需求。
* 如下示例，使用`ng-model`指令对数据进行绑定。
```
<div ng-app>
  请输入任意值：<input type="text" ng-model="name">
  你输入的为： {{ name }}
</div>
```

[slide]
#ng-model原理
1. angular加载完成之后会启动，首先找`ng-app`指令
2. 找到后认为`ng-app`里面的所有的内容都归angular来管
3. 找子层标签里所有的指令，然后就可以找到`ng-model`
4. 找到后会生成数据模型，然后挂在*作用域*上面
5. 使用此数据模型的*变量*和*视图*进行**绑定**


[slide]
##表达式
* 数据绑定，由两个花括号{{}}组成，可以把**数据绑定到HTML**，类似Javascript代码片段，可以包含文字、运算符和变量
* 输出变量的值
```html
<div ng-app ng-init="name='zfpx'">
      {{name}}
    </div>
```
* 进行表达式计算
```html
    <div ng-app ng-init="width=3;length=5">
     
    长方形的面积： {{ width * length }}
     
    </div>
```
* 输出对象的值
```html
  <div ng-app="" ng-init="numbers=['1','2','3']">  
    第一个数字为： {{ numbers[0] }}
    </div>
```

[slide]
##ng-controller
用这个指令在一个DOM元素上指定controller,控制器可能嵌套
```
<div ng-controller="AncestorController">
    {{ ancestorName }}
    {{ childName }}
    <div ng-controller="ChildController">
        {{ ancestorName }}
        {{ childName }}
    </div>
</div>
```

[slide]
##ng-bind
* `ng-bind`和`AngularJS`表达式功能相似，但`ng-bind`是在`angular`解析渲染完毕后才将数据显示出来的。
* 如下使用ng-bind指令绑定把应用程序数据。
```html
    <div ng-app="">
        请输入一个名字：<input type="text" ng-model="name">
        Hello <span ng-bind="name"></span>
         <span ng-bind="say"></span>
         <span ng-bind-html="say"></span>
         <span ng-bind-template="say"></span>
         <span ng-non-bindable="say"></span>
    </div>
```
> 使用花括号语法时，因为浏览器需要首先加载页面，渲染它，然后AngularJS才能把它解析成你期望看到的内容，所以对于首个页面中的数据绑定操作，建议采用ng-bind，以避免其未被渲染的模板被用户看到。


[slide]
##ng-init
* ng-init指令**初始化**应用程序数据，也就是为AngularJS应用程序定义初始值
* 如下所示，我们为应用程序变量name赋定初始值。
```angular
    <div ng-app="" ng-init="name='zfpx'">
    </div>
```
* 不仅可以赋值字符串，也可以赋值为数字、数组、对象，而且可以为多个变量赋初始值
```

[slide]
##ng-click
* AngularJS也有自己的HTML事件指令,比如说通过ng-click定义一个AngularJS单击事件。
* ng-click指令将DOM元素的鼠标点击事件(即mousedown)绑定到一个方法上，当浏览器在该DOM元素上鼠标触发点击事件时，Angular就会调用相应的方法。
* 对按钮、链接等，我们都可以用ng-click指令属性来实现绑定，如下简单示例：
```html
<div ng-app="" ng-init="click=false">
        <button ng-click="click= !click">隐藏/显示</button>
        <div ng-hide="click">
            请输入一个名字：<input type="text" ng-model="name">
            Hello <span ng-bind="name"></span> 
        </div>
    </div>
```
 PS：ng-hide="true"，设置HTML元素不可见。

[slide]
##ng-if
布尔类型 为true*执行*内部指令，为false时不执行内部指令
```
    <div ng-if="true">
        <span>show</span>
    </div>
```

[slide]
##ng-class
定义元素的`class`样式,属性值如 {'class1':expression1,'class2':expression2}
```
ng-class="{'has-error':username.length>6}"
```

[slide]
##ng-include
* `ng-include`就是将多个页面的公共页面提取出来，如`header.html`，`footer.html`等，在每个页面公用
```
 <div ng-include="'header.html'"></div>
```

[slide]
##ng-show
布尔类型 为true时*显示* false时隐藏
```
    <button ng-click="show = !show">切换</button>
    <div ng-show="show">ng-show欢迎来到珠峰培训</div>
```

[slide]
##ng-hide
布尔类型 为false时显示 true时*隐藏*
```
    <button ng-click="show = !show">切换</button>
    <div ng-hide="show">ng-hide欢迎来到珠峰培训</div>
```

[slide]
##ng-repeat
*遍历*数组
```
        <tr ng-repeat="item in items">
            <td>{{item.title}}</td>
            <td>{{item.price | currency}}</td>
            <td><input type="text" ng-model="item.quantity"/></td>
            <td>{{item.price*item.quantity | currency}}</td>
        </tr>
        <tr>
            <td>总金额 {{total()}}</td>
        </tr>
```


[slide]
##ng-readonly
通过表达式返回值true/false将表单输入字段设为只读。

```
<input type="text" ng-readonly="stop" value="3秒后禁用"/>
.run(function($rootScope,$timeout){
    $rootScope.stop=false;
    $timeout(function(){
        $rootScope.stop = true;
    },3000)
})
```

[slide]
##ng-checked
设置checkbox选中 
```
<input type="checkbox" ng-checked="someProperty" ng-init="someProperty = true" ng-model="someProperty">
```

[slide]
##ng-selected
给select里面的option用的
```
<label>
    <input type="checkbox" ng-model="other">
</label>
<select>
    <option>男</option>
    <option>女</option>
    <option ng-selected="other">其它!!!</option>
</select>
```

[slide]
##ng-switch
指令根据表达式显示或隐藏对应的部分。
对应的子元素使用 ng-switch-when 指令，如果匹配选中选择显示，其他为匹配的则移除。
你可以通过使用 ng-switch-default 指令设置默认选项，如果都没有匹配的情况，默认选项会显示。
```
element ng-switch="expression">
  <element ng-switch-when="value"></element>
  <element ng-switch-when="value"></element>
  <element ng-switch-when="value"></element>
  <element ng-switch-default></element>
element>
```

[slide]
##ng-href 
表达式生效前不要加载该资源
```
<a ng-href="{{ myHref }}">{{linkText}}</a>
.run(function($rootScope, $timeout) {
    $rootScope.linkText = '尚未加载，您无法点击';
    $timeout(function() {
        $rootScope.linkText = '请点击'
        $rootScope.myHref = 'http://www.baidu.com';
    }, 2000);
})
```
[slide]
##ng-src
表达式生效前不要加载该资源
```
<img ng-src="{{imgSrc}}"/>
.run(function($rootScope, $timeout) {
    $timeout(function() {
        $rootScope.imgSrc = 'https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo/bd_logo1_31bdc765.png';
    }, 2000);
})
```

[slide]
#表单验证
* 定义验证规则，验证有效性
* 显示验证结果
* 禁用html5自带验证 `novalidate="novalidate"`
* 用户输入后，angular会依次调用验证器进行验证，全部成功时model会变成用户输入的值
* 不成功时则保留原值，并在model上增加一个$error对象

[slide]
#成员变量
|变量名|含义|
|:-----|:----|
|$dirty| 表单中任何一项是否输入过|
|$pristine|表单中任何一项尚未输入过|
|$error|存放错误信息|
|$invalid|表单数据是否无效，只要有一项无效则整个表单无效|
|$valid|与$invalid相反|
|$name|表单的名字|
|email|表单各个输入框的model|

[slide]
#什么是MVC
- Model 数据<span class="text-danger">模型</span>层 {:&.rollIn}
- View <span class="text-danger">视图</span>层，负责展示
- Controller 业务逻辑和<span class="text-danger">控制</span>逻辑
[note]菜是模型 盘子是视图 服务员是控制器[/note]

[slide]
#为什么需要MVC
1. 代码规模越来越大，<span class="text-danger">切分责职</span> {:&.rollIn}
2. 相同逻辑代码要<span class="text-danger">复用</span>
3. 需求变更需要<span class="text-danger">重构</span>
4. 职责清晰，代码<span class="text-danger">模块化</span>
5. MVC只是手段，目标是<span class="text-danger">模块化</span>和<span class="text-danger">复用</span>
[note]盘子装很多不同的菜，活字印刷，有利于分工协作[/note]

[slide]
#Model模型使用
* MVC借助于*$scope*实现
* $scope是一个*基本*javascript对象
* $scope是一个*树型*结构，与DOM标签平行
* 子$scope对象遵循原型继承,会*继承*父$scope上的属性和方法
* 每一个angular应用只有一个*根*$rootScope对象(ng-app)上
* $scope是MVC和*双向数据绑定*的基础
* $scope是表达式的执行*上下文环境*
* 有自己的生命周期 创建->注册监控者->模型变化->检测变化->销毁
* $scope提供一些工具方法 *$watch/$apply*
* $scope可以*传播事件*，类似DOM事件，可以向上也可以向下传播

[slide]
#控制器
* ng-controller指令就是用来定义应用程序控制器的，并且同时创建了一个新的作用域关联到相应的DOM元素上
* 不要*复用*Controller,一个控制器只负责一个视图
* 不要在控制器中操作DOM，使用*指令*
* 不要在Controller里做数据*过滤和格式化*，使用filter过滤器
* 控制器之间不要互相直接调用，控制器之间的交互通过*事件*交互

[slide]
#模块化
* 模块化用来*分割*，组织和打包软件 {:&.rollIn}
* 每个模块完成一个特定的*子*功能
* 所有的模块按某种方法*组装*起来，成为一个整体，完成整个系统所要求的功能
* 一切是从模块开始，module就是容器,其它的元素都挂在module里面. 
* 模块是一些功能的集合，如控制器、服务、过滤器、指令等子元素组成的整体
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/angular-module.png" class="img-responsive">

[slide]
##模块之间如何依赖依赖注入
```
    //创建、获取angular中的模块
    angular.module(); 

    // 传递参数多于一个表示新建模块;空数组代表该模块不依赖其他模块
    var createModule = angular.module("myModule", []);

    // 只有一个参数(模块名),代表获取模块,如果模块不存在,angular框架会抛异常
    var getModule = angular.module("myModule");
    
    该函数既可以创建新的模块，也可以获取已有模块，是创建还是获取，通过参数的个数来区分。
    
    angular.module(name, [requires], [configFn]);
        
    - name：字符串类型，代表模块的名称；
    - requires：字符串的数组，代表该模块依赖的其他模块列表，如果不依赖其他模块，用空数组即可；
    - configFn：用来对该模块进行一些配置。
```

[slide]
##指令定义对象
* 每个指令定义的工厂函数，需要返回一个指令定义对象。
* 指令定义对象就是一个具有约定属性的JavaScript对象
* 指令定义对象的常用属性如下：

|配置项|类型|含义|
|:----|:----|:----|
|template|string|使用template指定的HTML标记替换指令内容（或指令自身）|
|restrict|string|用来限定指令在HTML模板中出现的位置|
|replace|true,false|是否替换原有的DOM元素|
|transclude|true,false,'element'|是否保留原有指令的内部元素|
|scope|true,false,{}|scope属性为指令创建私有的作用域|
|link|Function|link属性是一个函数，用来在指令中操作DOM树、实现数据绑定|

[slide]
##template 定义**替换**模板
* template指明一个HTML片段,可以用来替换指令的内容
* 如果replace = true，那么用HTML片段替换指令本身
* 如果transclue属性为true则包裹指令的内容

[slide]
##匹配模式restrict
----
|restrict|元素|用法|
|:----|:----|:----|
|E|元素|\<hello/>|
|A|属性|\<div hello></div>|
|C|样式类|\<div class="hello"></div>|
|M|注释|\<!-- directive:hello -->|
----
* 推荐使用元素和属性的方式使用指令
* *组件式*指令使用*元素*名称的方式创建指令
* *装饰型*指令使用*属性*的方式创建指令

[slide]
##replace
* replace属性指明使用template时，如何替换指令元素：
* true表示编译时，将使用template替换指令元素
* false表示编译时，将使用template替换指令元素的内容
 replace为true时，要求模板必须有一个根节点

[slide]
##transclude
* 有些指令需要能够包含其他未知的元素
* transclude属性可以告诉编译器，利用所在DOM元素的内容，替换template中包含 ng-transclude指令的元素的内容
```
    <dialog>
        <div>这里是指令内部的内容。</div>
    </dialog>
```
> 对话框的内容在我们开发dialog指令的时候是无法得知的，这部分内容需要被转移到展开的DOM树中适当的位置.

* 使用transclude有两个要点：
1. 需要首先声明transclude属性值为true,这将告诉编译器,使用我们这个指令的 DOM元素，其内容需要被复制并插入到编译后的DOM树的某个点。
2. 需要在template属性值中使用ng-transclude指明插入点

[slide]
##scope的绑定策略
----
|类型|用法|
|:----|:----|
|@|把当前属性作为字符串传递。你还可以绑定来自外层scope上的值，在属性中插入{{}}即可|
|=|与父scope中的属性进行双向绑定|

[slide]
#link:在指令中操作DOM
如果需要在指令中操作DOM，我们需要在对象中定义link属性
```javascript
function link(scope, iElement, iAttrs, controller, transcludeFn) { ... }
```
> 注意link函数的参数，AngularJS在编译时负责传入正确的值：

参数说明
----
|参数|含义|
|:----|:----|:----|
|scope|指令对应的scope对象。如果指令没有定义自己的本地作用域，那么传入的就是外部的作用域对象|
|iElement|指令所在DOM对象的jqLite封装。如果使用了template属性，那么iElement对应 变换后的DOM对象的jqLite封装|
|iAttrs|指令所在DOM对象的属性集。这是一个Hash对象，每个键是驼峰规范化后的属性名|
|controller|控制器的实例,在所有指令间共享,可以作为指令交流的通道|

[slide]
##指令的原理
1. 加载 加载angular.js,找到ng-app指令，确定应用的边界
2. 编译 遍历DOM，找到所有指令，根据指令中的template、replace和transclude转换DOM结构，如果存在`compile`函数就调用
3. 链接 对每个指令操作`link`函数,link函数一般用来操作DOM，绑定事件监听器


[slide]
##服务
服务是能提供特定*功能*的一个`对象`,有以下特点
1. service都是*单例*的 {:&.rollIn}
2. angular会*自动*创建实例并*注入*，不需要手工创建
3. service在整个应用的生命周期存在，可以*共享*数据

[slide]
##$http服务
$http是对jquery ajax的封装
```
        $http({
            method:'GET',
            url:'books.json'
        }).success(function(data,status,headers,config){
            $scope.books = data;
        }).error(function(data,status,headers,config){
                
        })
```

[slide]
##创建服务组件
* 在AngularJS中创建一个服务组件很简单，只需要定义一个具有$get方法的构造函数， 然后使用模块的provider方法进行登记：
```
    //定义构造函数
    var myServiceProvider = function(){
        this.$get = function(){
            return ....
        };
    };
    //在模块中登记
    angular.module("myModule",[]).provider("myService",myServiceProvider);
```

[slide]
##可配置的服务
* 有时我们希望服务在不同的场景下可以有不同的行为，这意味着服务可以进行配置。
```
    angular.module("myModule",[])
      .config(["myServiceProvider",function(myServiceProvider){
        
    }]);
```

> 注意：服务提供者provider对象在注入器中的登记名称是：服务名+Provider。 例如： $http的服务提供者实例名称是"$httpProvider"。

[slide]
##语法糖
使用模块的provider方法定义服务组件，在有些场景下显得有些笨重。AngularJS友好 地提供了一些简化的定义方法，这些方法通常只是对provider方法的封装， 分别适用于不同的应用场景：

* factory 使用一个对象工厂函数定义服务，调用该工厂函数将返回服务实例。
* service 使用一个类构造函数定义服务，通过new操作符将创建服务实例。
* value 使用一个值定义服务，这个值就是服务实例。
* constant 使用一个常量定义服务，这个常量就是服务实例。

[slide]
##factory方法
factory方法要求提供一个对象工厂，调用该类工厂将返回服务实例。
```
    var myServiceFactory = function(){
        return ...
    };
    angular.module("myModule",[])
    .factory("myService",myServiceFactory);
```
> AngularJS会将factory方法封装为provider，上面的示例等同于
```
var myServiceFactory = function(){
    return ...
};
angular.module("myModule",[]).provider("myService",function(){
    this.$get = myServiceFactory;
});
```

[slide]
##service方法
service方法要求提供一个构造函数，AngularJS使用这个构造函数创建服务实例：
```
    var myServiceClass = function(){
        this.method1 = function(){...}
    };
    angular.module("myModule",[]).service("myService",myServiceClass);
``` 
 AngularJS会将service方法封装为provider，上面的示例 等同于：
```
    var myServiceClass = function(){
      
    };
    angular.module("myModule",[]).provider("myService",function(){
        this.$get = function(){
            return new myServiceClass();
        };
    });
```

[slide]
##value
有时我们需要在不同的组件之间共享一个变量，可以将这种情况视为一种服务： provider返回的总是变量的值。
value方法提供了对这种情况的简化封装：

```
angular.module("myModule",[])
.value("myValueService","19841230");
```

> AngularJS会将value方法封装为provider，上面的示例 等同于：
```
angular.module("myModule",[])
.provider("myService",function(){
    this.$get = function(){
        return "19841230";
    };
});
```

[slide]
##constant方法
有时我们需要在不同的组件之间共享一个常量，可以将这种情况视为一种服务： provider返回的总是常量的值。
constant方法提供了对这种情况的简化封装：
```
angular.module("myModule",[])
    .constant("myConstantService","hello zfpx");
```
和value方法不同，AngularJS并没有将constant方法封装成一个provider，而仅仅 是在内部登记这个值。这使得常量在AngularJS的启动配置阶段就可以使用（创建任何 服务之前）：你可以将常量注入到模块的config()方法中。


[slide]
##过滤器
- filter是用来*数据格式化*的*服务*  {:&.rollIn}
- filter可以*级联*使用(用|分隔)
- filter是可以*传递参数*的

[slide]
##currency 货币过滤器
```javascript
{{ currency_expression | currency : symbol}}
{{amount | currency:"USD$"}}
```

[slide]
##date 日期过滤器
```javascript
{{ date_expression | date : format}}
<span ng-non-bindable>{{1288323623006 | date:'yyyy-MM-dd HH:mm:ss Z'}}</span>
```

[slide]
##json对象过滤器
```
{{ json_expression | json}}
<pre>{{ {'name':'value'} | json }}</pre>
```

[slide]
##limitTo限制过滤器
```
{{ limitTo_expression | limitTo : limit}}
{{ letters | limitTo:letterLimit }}
```

[slide]
##lowercase转成小写过滤器
```
{{ lowercase_expression | lowercase}}
{{'ABCDE'|lowercase}}
```

[slide]
##number数字过滤器
```
{{ number_expression | number : fractionSize}}
{{val | number:0}}
```

[slide]
##orderBy 排序
```
{{ orderBy_expression | orderBy : expression : reverse}}
$scope.predicate = '-age';
<tr ng-repeat="friend in friends | orderBy:predicate:reverse">
```

[slide]
##uppercase转大写
```
{{ uppercase_expression | uppercase}}
```

[slide]
##filter 
从一个数组集合中选择一个子集并返回一个新的数组
```
<table id="searchTextResults">
    <tr><th>Name</th><th>Phone</th></tr>
    <tr ng-repeat="friend in friends | filter:searchText">
        <td>{{friend.name}}</td>
        <td>{{friend.phone}}</td>
    </tr>
</table>
<hr>
任何属性: <input ng-model="search.$"> <br>
只匹配名称 <input ng-model="search.name"><br>
只匹配电话 <input ng-model="search.phone"><br>
必须相等 <input type="checkbox" ng-model="strict"><br>
<table id="searchObjResults">
    <tr><th>Name</th><th>Phone</th></tr>
    <tr ng-repeat="friendObj in friends | filter:search:strict">
        <td>{{friendObj.name}}</td>
        <td>{{friendObj.phone}}</td>
    </tr>
</table>
```

[slide]
##自定义filter
```
filter('strong',function(){
        return function(item,pre,tail){
            return pre+item + tail;
        }
    });
```

[slide]
##路由
不同的地址对应不同的页面和控制器
```
<script src="//cdn.bootcss.com/angular.js/1.3.0/angular-route.js"></script>
<a href="#/index">index</a>
<div ng-view></div>
angular.module('zfpxMod',['ngRoute']);
angular.module('zfpxMod').config(function($routeProvider){
    $routeProvider.when('/index',{
        templateUrl:'views/index.html',
        controller:'IndexCtrl'
    }).when('/user',{
        templateUrl:'views/user.html',
        controller:'UserCtrl'
    }).otherwise({
        redirectTo:'/index'
    });
});
```

[slide]
##$resource
$resource是一个创建资源对象的工厂,用来创建同服务端交互的对象
```
<script src="angular-resource.js"></script>
var Book = $resource('/books/:id', {id: '@id'}, {update: {method: 'PUT'}});
```
返回的Book对象包含了同后端服务进行交互的方法，我们可以把Book对象理解成同RESTFul的后端服务进行交互的接口。
```
 Book.query(); 查询所有的对象
 Book.delete(curr).$promise.then(function(result)) 删除一个对象
 Book.update($scope.book).$promise.then(function(result){}) 更新一个对象
 Book.save($scope.book).$promise.then(function(result){}) 保存一个对象
```

[slide]
##todo项目
http://fontawesome.dashgame.com/

