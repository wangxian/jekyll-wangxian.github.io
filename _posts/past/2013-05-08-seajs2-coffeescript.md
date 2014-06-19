---

layout: post
title: "尝试让Sea.js支持CoffeeScript"
tags:
  - JavaScript

---

在seajs 1.2， 1.3 版，有一个plugin-coffee 插件，可以支持`coffeescript`
写的模块，直接允许，在2.0版本，拿掉了 coffee plugin 故想试着开发一个plugin 插件。

seajs插件开发起来比较简单，又现成的例子可供参考。seajs2 本身带了好几个插件，所以
参考之；

plugin-coffee的原理是使用 CoffeeScript.load 来加载模块，编译`.coffee` 
插件开发完后，发现现实没有想象的那么美好。文件的load是需要用到xhr来加载，chrome
有同源限制，即使是`file:///` 也一样。(这也是一个不小的限制，现在开发的项目主要是本地运行。)

随放弃之。

后采用cake 来 watch觉得更简单。

_后来在coffeescript.org 上看到了这样的话_

> While it's not recommended for serious use …




附上源码：

### Cakefile
	
	# fs = require 'fs'
	
	{print} = require 'util'
	{spawn} = require 'child_process'
	
	# do like this: cake -o js watch ,
	# will output: { arguments: [ 'watch' ], output: 'js' }
	#
	# option '-o', '--output [DIR]', 'directory for compiled code'
	
	task 'watch', 'Watch and Compile [jsc DIR] output to [js DIR]', (options)->
	
	  coffee = spawn 'coffee', ['-wbco', 'js', 'jsc']
	
	  coffee.stderr.on 'data', (data)->
	    print data.toString()
	
	  coffee.stdout.on 'data', (data)->
	    print data.toString()

  process.on 'exit', (code)->
    print "Cake will exit(#{code})"

### plugin-coffee.js

	(function(seajs) {
	
	  seajs.on("resolve", function(data) {
	
	    var uri = seajs.resolve(data.id, data.refUri);
	    if ( /\.coffee.js$/.test(uri) ) {
	      uri = uri.replace(/\.js(?=$|\?)/, "");
	      data.uri = uri;
	    }
	
	    // console.log( uri );
	  });
	
	  seajs.on("request", function(data) {
	
	    if( /\.coffee$/.test(data.uri) ) {
	      data.requested = true;
	      // console.log(CoffeeScript);
	
	      CoffeeScript.load(data.uri);
	    }
	  });
	
	})(seajs);

