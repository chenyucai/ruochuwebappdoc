# 页面结构

系统由多个单页组成，下面以一个 `index` 单页实例为例子

> index.html

    <html>
      <head>
        <meta charset="utf-8">
        <meta name="renderer" content="webkit">
        <meta name="format-detection" content="telephone=no" />
        <title>首页</title>
        <link rel="stylesheet" href="css/index.css">
        <script type="text/javascript" data-main="js/main" data-start="index" src="js/lib/require.js"></script>
      </head>
      <body>
        <div class="page" id="page_a">  // a页面
          .....
        </div>

        <div class="page" id="page_b"> // b页面
          .....
        </div>

        <div class="page" id="page_c"> // c页面
          .....
        </div>

        ....

      </body>
    </html>

> index.js

    define(function(require, exports, module){
      var $ = require('zepto');
      var Backbone = require('backbone');
      var _ = require('underscore');
      var iScroll = require('iscroll');
      var config = require('config');
      var utils = require('utils');
      var wx = require('jweixin');

      document.addEventListener('touchmove', function (e) { e.preventDefault(); }, false);

      var PageA = function () {
        // 页面a的构造函数，页面a的代码逻辑都写在这里

        ....

      }

      var PageB = function () {
        // 页面b的构造函数，页面b的代码逻辑都写在这里

        ....

      }

      var PageC = function () {
        // 页面c的构造函数，页面c的代码逻辑都写在这里

        ....

      }

    }

    <!-- 路由 -->
    var AppRouter = Backbone.Router.extend({
      routes: {
        "": "res",
        "page_a": "page_a",
        "page_b":"page_b",
        "page_c":"page_c"
      },
      initialize: function(){
        this.pages = {
          page_a: undefined,
          page_a:undefined,
          page_a:undefined
        };
      },
      page_a: function(){
        this.pages.page_a = this.pages.page_a || new PageA();
      },
      page_b: function(){
        this.pages.page_b = this.pages.page_b || new PageB();
      },
      page_c: function(){
        this.pages.page_c = this.pages.page_c || new PageC();
      },
    });
