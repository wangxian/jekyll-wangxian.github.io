---

layout: post
title: "实战AngularJS开发"
comments: true
category: weeklog
tags: 
  - JavaScript
  - Angular.js
  - weeklog
  
---


<img class="cover" src="http://ww4.sinaimg.cn/large/493b785ajw1e83paupkp7j20an03074c.jpg" alt="" />

过年的时候，研究过Angular.js 这个还算大名鼎鼎的js库，还写了一篇blog, \\
[『\[学习笔记\]Angular.js学习笔记与感悟』](/2013/02/angular-js.html)

但没动手试过，怎么来开发一个todo的小应用。

开发angular.js应用，不用你从零开始，要么说大公司维护的框架不一样呢（Supper Google），angularjs的文档就不说了，
详细的开发文档，看的都让你觉得头疼，入门有一个AngularJS Totour「angularjs-phonecat」，
然后有一个开发说明 Developer Guide，最后还有一个 Api Reference，把这些玩意儿看完，都需要好长时间。

OK，现在来动手来开发一个angularjs todo App, angularjs 提供了一个seed， 你可以从这个seed开始。

Angularjs seed on Github. <https://github.com/angular/angular-seed>

把seed中包含：`LICENSE README.md app/ config/ index.html logs/ scripts/ test/`
app目录里是app的主程序，script有nodejs的webserver方便开发，原因是因为angularjs views，你懂的。

app/目录里有2个html, index.html, index-async.html(异步加载js) 


## index.html

    <!doctype html>
    <html lang="zh_CN" id="ng-app" ng-app="myApp">
    <head>
      <meta charset="utf-8">
      <title>My Todo</title>
      <link rel="stylesheet" href="css/reset.css"/>
      <link rel="stylesheet" href="css/app.css"/>
    </head>
    <body>
    <div class="page">
      <div class="header box">
        <a href="index.html"><h1>My Todo</h1></a>
      </div>

      <div class="main box" ng-view>

      </div>

      <div class="foot">
        Copyright &copy; <a href="http://wangxian.me">wangxian.me</a> 木頭 <br />
        一个简易的 todo 程序(方案: Github+AngularJS+JSON3)
        directive V<em app-version></em>, value: {{ 'Current version is v%VERSION%' | interpolate }}
      </div>

    </div>

    <!--[if lt IE 8]>
    <script type="text/javascript" src="http://bestiejs.github.io/json3/lib/json3.min.js"></script>
    <![endif]-->

    <!-- In production use:
    <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
    -->

    <script src="lib/angular/angular.js"></script>
    <script src="js/app.js"></script>
    <script src="js/services.js"></script>
    <script src="js/controllers.js"></script>
    <script src="js/filters.js"></script>
    <script src="js/directives.js"></script>

    </body>
    </html>

首页是一个layout，和加载资源的作用。


## 列表视图：partials/list.html
    <div class="box post">
      <p><input type="text" placeholder="Create a new Todo." name="title" class="submit" ng-enter="newTodo($event)"></p>
    </div>

    <div class="box todos">
      <h2 class="box">待办事项</h2>
      <ul>
        <li class="item" ng-repeat="x in list | orderBy:'date':true">
          <span ng-class="itemClass(x.finished)">{{x.title}}</span>
          <span class="date">({{x.date | date:'yyyy-MM-dd HH:mm:ss'}})</span>
          <a href="" ng-click="gotoEdit(x)">编辑</a>
          <a href="" ng-show="! x.finished" ng-click="itemFinished(x)">完成</a>
          <a href="" ng-show="x.finished" ng-click="itemRenew(x)">恢复</a>
          <a href="" ng-click="itemDelete(x)">删除</a>
        </li>
      </ul>
    </div>

## 编辑视图：partials/edit.html
    <div class="box post">
      <h2>编辑</h2>
      <p><input type="text" class="submit" ng-enter="itemUpdate($event)" ng-model="title" value="{{title}}"></p>
      <p>回车提交</p>
    </div>


## app/js/app.js
    // Declare app level module which depends on filters, and services
    angular.module('myApp', ['myApp.filters', 'myApp.services', 'myApp.directives', 'myApp.controllers']).
      config(['$routeProvider', '$locationProvider', function($routeProvider, $locationProvider) {
        $routeProvider.when('/list', {templateUrl: 'partials/list.html', controller: 'ListCtrl'});
        $routeProvider.when('/edit/:id', {templateUrl: 'partials/edit.html', controller: 'EditCtrl'});
        $routeProvider.otherwise({redirectTo: '/list'});

        $locationProvider.html5Mode(false).hashPrefix("!");
      }]);
    
定义Angularjs路由，使用了`$locationProvider`, 关闭了html5的URL，启用hashbang的方式的URL。
首页url，`./index.html#!/list`, 编辑URL，`./index.html#!/edit/120`， 如果不满足
上面的2个URL，则跳转到 `./index.html#!/list`。

并且指定list对应的控制器，ListCtrl， 编辑页的控制器 EditCtrl


## app/js/controllers.js

    // 把todo信息存储在变量中
    var list = [
      {
        "id"      : 1,
        "title"   : "安装mongoskin模块，npm install mongoskin",
        "date"    : 1286461782373,
        "finished": 0
      },
      {
        "id"      : 2,
        "title"   : "测试本地条已完成!",
        "date"    : 1276461782373,
        "finished": 1
      }
    ];

    angular.module('myApp.controllers', []).
      controller('ListCtrl', ['$scope', '$location', "opt", "alert", function($scope, $location, opt, alert) {

        $scope.list = list
        
        // 每条记录的class
        $scope.itemClass = function (finished) {
          // console.log("new:", finished)
          return finished ? "del" : "new"
        }

        // 点击完成，设置为已完成，会自动更新view，为已完成。
        $scope.itemFinished = function (item) {
          // console.log(item)
          item.finished = 1
        }

        // 重新设置为 未完成
        $scope.itemRenew = function(item) {
          item.finished = 0;
        }

        // 删除item
        $scope.itemDelete = function(item) {
          for(var i=0, len=$scope.list.length;i<len;i++) {
            if(item === $scope.list[i]) {
              $scope.list.splice(i, 1);
            }
          }
        }

        // 添加todo
        $scope.newTodo = function(e) {
          var data = {}
          data.id = this.list.length+1;
          data.title = e.target.value;
          data.finished = 0
          data.date = (new Date()).getTime()

          this.list.push(data)
        }

        // 编辑todo item
        $scope.gotoEdit = function(item){
          $location.url("/edit/"+ item.id)
        }
      }])


      .controller('EditCtrl', ['$scope', '$routeParams', '$location', function($scope, $routeParams, $location) {
        // console.log($routeParams)
        // console.log(list)
        var _data = list[ $routeParams.id - 1 ];
        $scope.title = _data.title;

        // 当在编辑框中，回车提交后，更新todo, 并回到首页
        $scope.itemUpdate = function(e) {
          _data.title = $scope.title;
          $location.url("/list")
        }

      }]);


上面是angularjs-todo的关键代码，实现一个简单的应用，用angularjs，非常方便，angularjs为一个独立的库
并且自带jqLite, 简易的jquery，基本上不用依赖第三方库，关于模板，可以看到angularjs本身就模板，典型的
DOM 模板型。

Angularjs最关键的技术就数依赖注入了，DI系统，DI系统帮你做了很多事情。

用angularjs和别的库，最不一样的地方，在写HTML的时候，模板就出来了，要注意HTML和控制器的交互。
按照angularjs的思想去做页面。

如果遇到复杂的逻辑，可以封装成services，由于上面的例子比简单，所以就没把todo存储操作进行封装，放到了内存中。

    /* Services Example */
    angular.module('myModule', []).
     value('a', 123).
     factory('a', function() { return 123; }).
     directive('directiveName', ...).
     filter('filterName', ...);

Angularjs的services主要是有以上几种。

所以用angularjs开发单页应用，非常简单，文档什么都比较全。
只是现在国内用的不多，国内用的最多的还是`backbone.js` 。

还有Angularjs默认支持IE8+, 不过很容易解决，[Develop Guide上提供了解决办法](http://docs.angularjs.org/guide/ie)。


上面的angularjs-todo 已经放到了Github上。\\
地址：<https://github.com/wangxian/angularjs-todo>\\
在线演示：<http://wangxian.me/angularjs-todo>






