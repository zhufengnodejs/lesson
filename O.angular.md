title: O. Angular.js
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
##双向数据绑定
1. <span class="text-danger">数据</span>变化响应*界面显示* {:&.rollIn}
2. <span class="text-danger">UI</span>变化影响*数据*
3. `ng-model` 将`$scope`变量与*输入框*绑定

[slide]
##ng-bind
绑定*html*元素
```
<span ng-bind="say"></span>
```

[slide]
##ng-click
为当前元素<span class="text-danger">click</span>事件绑定`$scope`上的对应方法
```
    <span ng-bind="say"></span>
    <span ng-click="show(say)">show</span>
```

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
##自定义服务
可以用模块的factory方法定义自己的服务
```
angular.module('appModule').factory('bookService',function(){
        var booklist = ['angular','node.js'];
        return {
            list:function(){
                return booklist;
            },
            add:function(bookname){
                booklist.push(bookname);
                return booklist;
            }
        }
    });
```


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
##firebase
Firebase是一个提供实时数据的云服务平台，你只需要将你的数据存放在Firebase上，就可以通过它提供的接口来实现实时数据同步

1. 注册并创建一个Firebase账户
2. 引入firebase脚本到页面
3. 添加模块依赖
4. 依赖注入firebase服务
5. 数据同步
```
var base = new Firebase('https://sizzling-heat-3542.firebaseio.com/contacts');
```

firebase https://www.firebase.com/docs/
angularfire https://www.firebase.com/docs/web/bindings/angular/api.html?utm_medium=web&utm_source=angularfire
angularfire https://github.com/firebase/angularfire


[slide]
##用法
1. $add(value) 增加一个元素
2. $remove(key) 删除一个元素
3. $save(key) 保存元素

[slide]
##todo项目
http://fontawesome.dashgame.com/
##聊天室项目
