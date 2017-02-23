# backbone.js

> Backbone定义一组小而高效的集合，包括了数据结构（models（模型） 和 collections（集合））和用户接口（views（视图） 和 URLS），是一款小巧的MVC框架

目前的框架使用的技术栈为：__require.js + backbone.js + router + zepto + underscore__

使用单页模式去构建 __单页应用（SPA）__ ，目前系统由多个单页构成


> 使用方法

#### Backbone.Model（模型）

Models（模型）包括数据交互及与其相关的大量逻辑： 转换、验证、计算属性和访问控制。你可以用特定的方法扩展

    var Sidebar = Backbone.Model.extend({
      promptColor: function() {
        var cssColor = prompt("Please enter a CSS color:");
        this.set({color: cssColor});
      }
    });

    window.sidebar = new Sidebar;

    sidebar.on('change:color', function(model, color) {
      $('#sidebar').css({background: color});
    });

    sidebar.set({color: 'white'});

    sidebar.promptColor();



#### Backbone.Collection（集合）

集合是模型的有序组合，我们可以在集合上绑定 "change" 事件，从而当集合中的模型发生变化时fetch（获得）通知，集合也可以监听 "add" 和 "remove" 事件， 从服务器更新，并能使用 Underscore.js 提供的方法。

集合中的模型触发的任何事件都可以在集合身上直接触发，所以我们可以监听集合中模型的变化： `documents.on("change:selected", ...)`

#### __model__      _collection.model_

覆盖此属性来指定集合中包含的模型类。可以传入原始属性对象（和数组）来 `add`, `create`,和 `reset`，传入的属性会被自动转换为适合的模型类型。

    var Library = Backbone.Collection.extend({
      model: Book
    });

集合也可以包含多态模型，通过用构造函数重写这个属性，返回一个模型。

    var Library = Backbone.Collection.extend({

      model: function(attrs, options) {
        if (condition) {
          return new PublicDocument(attrs, options);
        } else {
          return new PrivateDocument(attrs, options);
        }
      }

    });


#### Backbone.View（视图）

Backbone配合使用任何JavaScript模板库渲染界面（目前系统使用的是`underscore`的`template`。 一般是组织您的接口转换成逻辑视图， 通过模型的支持， 模型变化时， 每一个都可以独立地进行更新， 而不必重新绘制该页面。我们再也不必钻进 JSON 对象中，查找 DOM 元素，手动更新 HTML 了，通过绑定视图的 render 函数到模型的 "change" 事件 — 模型数据会即时的显示在 UI 中。

`extendBackbone.View.extend(properties, [classProperties]) `
开始创建自定义的视图类。 通常我们需要重载 render 函数，声明 events， 以及通过 tagName, className, 或 id 为视图指定根元素。

    var DocumentRow = Backbone.View.extend({

      tagName: "li",

      className: "document-row",

      events: {
        "click .icon":          "open",
        "click .button.edit":   "openEditDialog",
        "click .button.delete": "destroy"
      },

      initialize: function() {
        this.listenTo(this.model, "change", this.render);
      },

      render: function() {
        ...
      }

    });

直到运行时， `像tagName`, `id`, `className`, `el`, 和 `events`这样的属性也可以被定义为一个函数.

> 参考资料

- backbone.js: [http://www.css88.com/doc/backbone/][1]

[1]: http://www.css88.com/doc/backbone/ "backbone"
