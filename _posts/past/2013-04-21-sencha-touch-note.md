---

layout: post
title: "Sencha Touch Dev"
categories:
    - "sencha"

---

## 生成项目 Init Project

1. 进入sencha sdk 目录, `eg: cd touch-2.2.1/`
2. 执行 `sencha generate app projectName ../projectPath`


## 生成model
	sencha generate model User id:int


## 构建production应用
	sencha app build production


## 构建native包
	sencha app build native


### About APP build
- testing - intended for QA prior to production. All JavaScript and CSS source files are bundled, but not minified, which makes it easier to debug.

- package - creates a self-contained, redistributable production build that normally runs from the local file system without a web server.

- production - creates a production build that is normally hosted on a web server and serves multiple clients (devices). The build is offline-capable using HTML 5 application cache, and is enabled to perform over-the-air updates.

- native - first generates a package build, then packages it as a native application, ready to be deployed to native platforms.



## 这也行? 还能直接掉起来iOS模拟器
	sencha app package run packager.json

然后真的调用起来了一个模拟器了，真是非常的方便。而且生成以后，不用配置。
默认 `packager.json` 里的 platform 是 `iOSSimulator`


----------------------------------------------------------------

## Controller

有个比较重要的，routers & refs


	Ext.define('MyApp.controller.Main', {
	    extend: 'Ext.app.Controller',

	    config: {
	        control: {
	            loginButton: {
	                tap: 'doLogin'
	            },
	            'button[action=logout]': {
	                tap: 'doLogout'
	            }
	        },

	        refs: {
	            loginButton: 'button[action=login]'
	        }
	    },

	    doLogin: function() {
	        // called whenever the Login button is tapped
	    },

	    doLogout: function() {
	        // called whenever any Button with action=logout is tapped
	    }
	});




理解上refs 是引用的别名，control 类似 backbone的 events 的事件绑定。


---------------------------------------------------

## Views

创建一个view


	Ext.create('Ext.Panel', {
	  html: 'Welcome to my app - 王见',
	  fullscreen: true
	});


或先define一个，然后create


	Ext.define('MyApp.view.Welcome', {
	    extend: 'Ext.Panel',

	    config: {
	        html: 'Welcome to my app',
	        fullscreen: true
	    }
	});

	Ext.create('MyApp.view.Welcome');


下面是官方提供的一个twitter图片展示的完整示例，
注意: config, element, initialize， on 的使用。

	Ext.define('MyApp.view.Image', {
	   extend: 'Ext.Img',

	   config: {
	       title: null,
	       description: null
	   },

	   //sets up our tap event listener
	   initialize: function() {
	       this.callParent(arguments);

	       this.element.on('tap', this.onTap, this);
	   },

	   //this function is called whenever you tap on the image
	   onTap: function() {
	       Ext.Msg.alert(this.getTitle(), this.getDescription());
	   }
	});

	//creates a full screen tappable image
	Ext.create('MyApp.view.Image', {
	   title: '图片标题',
	   description: '这里是图片信息',

	   src: 'http://apod.nasa.gov/apod/image/1202/oriondeep_andreo_960.jpg',
	   fullscreen: true
	});



必须在initialize中调用 `this.callParent(arguments);` 来继承父类，
不然组件可能运行不正常。

每一个view等组件上，都有一个element方法，可以添加事件等；


### 视图隐式 setXXX getXXX applyXXX updateXXX

- 上一个例子中，在view中会自动生成getTitle, setTitle等，也就是getter，and setter

- applyXXX 当set发生变化的时候，或当第一次初始化的时候，也会调用。常用来修改变化的值，如把`10`组装成`10px solid dashed`

- updateXXX 当调用完applyXXX后，接着调用updateXXX。常用来把改变的值反应到dom上。


示例：

	// as before
	Ext.define('MyApp.view.MyView', {
	    extend: 'Ext.Panel',

	    config: {
	        border: 0
	    },

	    applyBorder: function(value) {
	        return value + "px solid red";
	    },

	    updateBorder: function(newValue, oldValue) {
	        this.element.setStyle('border', newValue);
	    }
	});

	// create an instance of MyView with a
	// spinner field that updates the border config
	var view = Ext.create('MyApp.view.MyView', {
	    border: 5,
	    fullscreen: true,
	    styleHtmlContent: true,
	    html: 'Tap the spinner to change the border config option',
	    items: {
	        xtype: 'spinnerfield',
	        label: 'Border size',
	        docked: 'top',
	        value: 5,
	        minValue: 0,
	        maxValue: 100,
	        increment: 1,
	        listeners: {
	            spin: function(spinner, value) {
	                view.setBorder(value);
	            }
	        }
	    }
	});



# Device Profiles

为了适应不同尺寸的屏幕，需要检测设备，并且加载不同的类，

需要在`app.js`中定义

	Ext.application({
	    name: 'Mail',

	    profiles: ['Phone', 'Tablet'],
	    models: ['User'],
    	views: ['Navigation', 'Login']
	});



Phone定义在, `app/profile/Phone.js`

	Ext.define('Mail.profile.Phone', {
	    extend: 'Ext.app.Profile',

	    config: {
	        name: 'Phone',
	        views: ['Main']
	    },

	    isActive: function() {
	        return Ext.os.is('Phone');
	    }
	});




文件的加载顺序：

1. app/model/User.js
2. app/view/Navigation.js
3. app/view/Login.js
4. app/view/phone/Main.js



可以看到在profile中定义的最后加载。

可以用`Ext.os.is`来判断设备是Phone还是Tables

并且在profile中定义的load view，是在当前profile名字下的目录里，如`app/view/phone/Main.js` 如果需要同样在view/Main.js 中，那在config.views 中写全路径：`Mail.view.Main`


### The Launch Process

APP初始化顺序

1. Controllers are instantiated; each Controller's init function is called

2. The Profile's launch function is called
3. The Application's launch function is called.


不同的设备可以定义不同的views, controllers, models

不同的views：

	Ext.define('Mail.view.tablet.Main', {
	    extend: 'Ext.Container',

	    config: {
	        layout: 'fit',
	        items: [
	            {
	                xtype: 'messagelist',
	                width: 200,
	                docked: 'left'
	            },
	            {
	                xtype: 'messageviewer'
	            }
	        ]
	    }
	});

	Ext.define('Mail.view.phone.Main', {
	    extend: 'Ext.Container',

	    config: {
	        layout: 'card',
	        items: [
	            {
	                xtype: 'messagelist'
	            },
	            {
	                xtype: 'messageviewer'
	            }
	        ]
	    }
	});


详细见 <http://docs.sencha.com/touch/2.2.0/#!/guide/profiles>


# History 支持

**简单匹配**

	Ext.define('MyApp.controller.Products', {
	    extend: 'Ext.app.Controller',

	    config: {
	        routes: {
	            'products/:id': 'showProduct',
	            'products/:id/:format': 'showProductInFormat'
	        }
	    },

	    showProduct: function(id) {
	        console.log('showing product ' + id);
	    },

	    showProductInFormat: function(id, format) {
	        console.log('showing product ' + id + ' in ' + format + ' format');
	    }
	});

**复杂匹配**

	Ext.define('MyApp.controller.Products', {
	    extend: 'Ext.app.Controller',

	    config: {
	        routes: {
	            'file/:filename': {
	                action: 'showFile',
	                conditions: {
	                    ':filename': "[0-9a-zA-Z\.]+"
	                }
	            }
	        }
	    },

	    //opens a new window to show the file
	    showFile: function(filename) {
	        window.open(filename);
	    }
	});

复杂匹配的时候，需要把router定义为object，action为处理方法。

*感觉：* 没有backbone 方便，直接定义正则表达式，不过这感觉和controller的refs controller的感觉差不多。

**Restore state and deep link**

such as http://myapp.com/#products/123

	Ext.define('MyApp.controller.Products', {
	    extend: 'Ext.app.Controller',

	    config: {
	        refs: {
	            main: '#mainView'
	        },

	        routes: {
	            'products/:id': 'showProduct'
	        }
	    },

	    /**
	     * Endpoint for 'products/:id' routes. Adds a product details view (xtype = productview)
	     * into the main view of the app then loads the Product into the view
	     *
	     */
	    showProduct: function(id) {
	        var view = this.getMain().add({
	            xtype: 'productview'
	        });

	        MyApp.model.Product.load(id, {
	            success: function(product) {
	                view.setRecord(product);
	            },
	            failure: function() {
	                Ext.Msg.alert('Could not load Product ' + id);
	            }
	        });
	    }
	});


例子中将从服务器端获取数据。

router可以被 `Device Profile` 重写。

eg:

	Ext.define('MyApp.controller.Products', {
	    extend: 'Ext.app.Controller',

	    config: {
	        routes: {
	            'products/:id': 'showProduct'
	        }
	    }
	});
	Ext.define('MyApp.controller.phone.Products', {
	    extend: 'MyApp.controller.Products',

	    showProduct: function(id) {
	        console.log('showing a phone-specific Product page for ' + id);
	    }
	});
	Ext.define('MyApp.controller.tablet.Products', {
	    extend: 'MyApp.controller.Products',

	    showProduct: function(id) {
	        console.log('showing a tablet-specific Product page for ' + id);
	    }
	});

### Application Dependencies

定义在application 里的views, models, controllers

	Ext.application({
	    name: 'MyApp',

	    views: ['Login'],
	    models: ['User'],
	    controllers: ['Users'],
	    stores: ['Products'],
	    profiles: ['Phone', 'Tablet']
	});


会加载以下文件：

* app/view/Login.js
* app/model/User.js
* app/controller/Users.js
* app/store/Products.js
* app/profile/Phone.js
* app/profile/Tablet.js

用 `Ext.require` 也是可以的

	Ext.require([
	    'MyApp.view.Login',
	    'MyApp.model.User',
	    'MyApp.controller.Users',
	    'MyApp.store.Products',
	    'MyApp.profile.Phone',
	    'MyApp.profile.Tablet'
	]);


且在profile中也可以定义，eg:

	Ext.define('MyApp.profile.Tablet', {
	    extend: 'Ext.app.Profile',

	    config: {
	        views: ['SpecialView'],
	        controllers: ['Main'],
	        models: ['MyApp.model.SuperUser']
	    },

	    isActive: function() {
	        return Ext.os.is.Tablet;
	    }
	});

classes在多个子目录里：

	Ext.application({
	    name: 'MyApp',

	    controllers: ['Users', 'nested.MyController'],
	    views: ['products.Show', 'products.Edit', 'user.Login']
	});

或定义一个 外部的公共 Auth 引用。(个人理解，是多个app公用一个Auth文件夹)

	Ext.Loader.setPath({
	    'Auth': 'Auth'
	});

	Ext.application({
	    views: ['Auth.view.LoginForm', 'Welcome'],
	    controllers: ['Auth.controller.Sessions', 'Main'],
	    models: ['Auth.model.User']
	});

会加载以下文件，感觉有点controller, refs 的影子，注意需要用 `Ext.Loader.setPath` 来指定auth目录。

* Auth/view/LoginForm.js
* Auth/controller/Sessions.js
* Auth/model/User.js
* app/view/Welcome.js
* app/controller/Main.js

最好把view或controllers 的依赖定义在view本真中，不要放在 app.js 中，
保持app.js的清晰。

完整示例：

    // app/views/Main.js
	Ext.define('MyApp.view.Main', {
	    extend: 'Ext.Container',

	    requires: [
	        'MyApp.view.Navigation',
	        'MyApp.view.MainList'
	    ],

	    config: {
	        items: [
	            {
	                xtype: 'navigation'
	            },
	            {
	                xtype: 'mainlist'
	            }
	        ]
	    }
	});

	// app.js
	Ext.application({
	    views: ['Main']
	});

	// this is bad approach
	Ext.application({
	    views: ['Main', 'Navigation', 'MainList']
	});





