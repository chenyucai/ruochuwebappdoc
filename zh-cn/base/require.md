# require.js

> 目前代码模块化管理用的是 _requirejs_ , RequireJS以一个相对于baseUrl的地址来加载所有的代码。 页面顶层`<script>`标签含有一个特殊的属性data-main，require.js使用它来启动脚本加载过程，而baseUrl一般设置到与该属性相一致的目录

    <script data-main="scripts/main.js" src="scripts/require.js"></script>

##### 一般会在项目里创建一个 `main.js` 文件去管理依赖的js文件

    require.config({
      baseUrl: "js",
      shim: {
        'underscore': {exports: '_'},
        'zepto': {exports: '$'},
        'backbone': {exports: 'Backbone', deps: ['underscore', 'zepto']},
        'iscroll': {exports:'iScroll'},
        'ikeyboard': {exports:'Keyboard', deps:['zepto']},
        'yctimer': {exports:'yctimer', deps:['zepto']},
        'swipeSlide': {exports:'swipeSlide', deps:['zepto']},
        'mdatetimer': {exports:'mdatetimer', deps:['zepto']},
        'mobiscroll': {exports:'mobiscroll', deps:['zepto','mobiscroll.scroller']},
        'jweixin': {exports:'wx'}
      },
      paths: {
        "jweixin": "http://res.wx.qq.com/open/js/jweixin-1.0.0",
        "zepto":   "lib/zepto.min",
        "underscore": "lib/underscore.min",
        "backbone": "lib/backbone.min",
        "iscroll":"lib/iscroll.min",
        "ikeyboard":"lib/iKeyboardScroll4",
        "yctimer":"lib/yctimer",
        "swipeSlide": "extend/swipeSlide/swipeSlide",
        "mobiscroll": "extend/mobiscroll/mobiscroll.min",
        "mobiscroll.scroller": "extend/mobiscroll/mobiscroll.scroller.min",
        "config": "config",
        "utils":"utils.2.0"
      },
      waitSeconds: 0
    });

    require(["zepto","utils"],function($, utils){
      $(function(){
        var token = utils.url.get('token');
        if (token != null) {
          utils.local.set('token', token);
        }
        var startModuleName = $("script[data-main][data-start]").attr("data-start");
        if (startModuleName) {
          require([startModuleName]);
        }
      });
    });

##### 然后在每个页面引入

    <script type="text/javascript" data-main="js/main" data-start="chemo_res"  src="js/lib/require.js"></script>

`chemo_res.js` 则是这个页面所需要的js文件


> 参考资料


require.js: [http://www.requirejs.cn/][1]

[1]: http://www.requirejs.cn/ "require"
