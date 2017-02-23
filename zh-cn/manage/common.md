# 公共函数

动态生成左边菜单栏，具体需要在config.js里面去配置

    function filterMenu(nav, M, R) {
      var filterNav = [];
      $.each(nav,function(i,v){
        var menuIn = false;
        var menuObj = {};
        menuObj.modules = [];
        $.each(v.modules, function(i,mod){
          if (mod.standard === true || (validate_M(mod.key, M) && validate_R(mod.roles, R))) {
            var modObj = {name:mod.name, url:mod.url};
            menuObj.modules.push(modObj);
            menuIn = true;
          }
        });
        if (menuIn) {
          menuObj.id = v.id;
          menuObj.name = v.name;
          menuObj.icon = v.icon;
          filterNav.push(menuObj);
        }
      });
      var FILTERMENU = config.MENU;
      FILTERMENU.nav = filterNav;
      storage.localStorage.set("FILTERMENU",FILTERMENU);
    }

    function init_menu(activeId){
      var operator = storage.localStorage.get('operator');
      var filtermenu = storage.localStorage.get('FILTERMENU');
      $("#LOGO").html(filtermenu.logoName);
      $("#WELCOME").html(operator.organName);
      $.each(filtermenu.nav, function(i,v){
        var c = $("#template").clone(true);
        c.removeAttr("style");
        c.attr("id",v.id);
        c.find("i").addClass(v.icon);
        c.find(".nav-label").html(v.name);
        $("#side-menu").append(c);
        if(v.id == activeId){
          c.addClass("active");
          c.find(".nav-second-level").addClass("in").attr("aria-expanded","true");
        }
        $.each(v.modules, function(j,mod){
          var a = $('<li><a href=""></a></li>');
          c.find(".nav-second-level").append(a);
          a.find("a").html(mod.name).attr("href",mod.url);
        });
      });

      var acc = filtermenu.operator;
      var accHtml = "";
      $.each(acc, function(i,v){
        accHtml += '<li><a href="'+v.url+'" onclick="'+v.onclick+'">'+v.name+'</a></li>';
      });
      $("#accDrop").html(accHtml);
      var nameTxt = storage.localStorage.get("operator").name;
      $("#accName").html(nameTxt != "" ? nameTxt : "管理员");
    }

>jqGrid(tableSelector, pagerSelector, options)

tableSelector为表格选择器，pagerSelector为页面选择器，options为对象，默认defaults

    var defaults = {
      datatype: "json",  //数据类型
      height: "auto",
      autowidth: true,
      add: true,        //设为true则有新增按钮
      import:false,     //导入按钮
      export:false,     //导出按钮
      delMults: true,
      multiselect:true,
      rowNum: 15,       //表格每页显示的数量
      rowList: [15,30,60],      //表格数量选择框
      pager: pagerSelector,
      viewrecords: true,
      caption: '',
      addName:'新增',    //新增按钮的名字
      importName:'导入',      //导入按钮的名字
      exportName:'导出表格',  //导出按钮的名字
      mtype : "post",       //数据传输类型(相当于ajax  type)
      hiddengrid: false,
      hidegrid:true,
      open: false,      //开启按钮
      close: false,     //关闭按钮
      prmNames: {page:'page',rows:'rows', sort: null,order: null, search:null, nd:null, npage:null},
      postData: {
        startPage:1
      }         //自定义传递参数

      $(tableSelector).jqGrid({   //设置表格的属性
        url: opts.url,
        datatype: opts.datatype,
        height: opts.height,
        autowidth: opts.autowidth,
        multiselect: opts.multiselect,
        rowNum: opts.rowNum,
        rowList: opts.rowList,
        colNames: opts.colNames,
        colModel: opts.colModel,
        pager: opts.pager,
        viewrecords: opts.viewrecords,
        caption: opts.caption,
        mtype : opts.mtype,
        hiddengrid: opts.hiddengrid,
        hidegrid: opts.hidegrid,
        jsonReader: opts.jsonReader,
        ajaxGridOptions:{
          headers:{token: storage.localStorage.get('token')}
        }

单选按钮，复选框的各种方法

    function getRadioValue(name){
      var obj = document.getElementsByName(name);
      var radio_val = "";
      for(k in obj){
        if (obj[k].checked) {
          radio_val = obj[k].value;
        }
      }
      return radio_val;
    }

    function setRadioByValue(name,value){
      var obj = document.getElementsByName(name);
      for(k in obj){
        if (obj[k].value == value) {
          obj[k].checked = true;
          a = 1;
          break;
        }
      }
    }

    function setCheckboxByValue(name,arr){
      var obj = document.getElementsByName(name);
      for(k in obj){
        for (var i = 0; i < arr.length; i++) {
          if (obj[k].value == arr[i]) {
            obj[k].checked = true;
          }
        }
      }
    }

    function clearRadioValue(name){
      $("input[type=radio][name="+name+"]").each(function(){
        $(this).prop('checked',false);
      });
    }

    function getCheckBoxValue(name){
      obj = document.getElementsByName(name);
      check_val = [];
      for(k in obj){
        if(obj[k].checked)
          check_val.push(obj[k].value);
      }
      return check_val;
    }

    function setAllChecked(name){
      var selector = "input[name="+name+"]";
      $(selector).each(function(i){
        $(this).prop("checked",true);
      });
    }

    function setAllUnchecked(name){
      var selector = "input[name="+name+"]";
      $(selector).each(function(i){
        $(this).prop("checked",false);
      });
    }

数组转字符串

    function arrayToString(arr) {
      var str = "";
      if (typeof(arr) != null && arr.length != 0) {
        for (var i = 0; i < arr.length; i++) {
          if (i == arr.length-1) {
            str += arr[i];
          }else {
            str += arr[i] + "，";
          }
        }
      }
      return str;
    }

字符串转数组

    function stringToArray(str){
      var arr = [];
      if (str.indexOf(' ') > 0) {
        arr = str.split(' ');
        return arr;
      }
      if (str.indexOf(',') > 0) {
        arr = str.split(',');
        return arr;
      }
      if (str.indexOf('，') > 0) {
        arr = str.split('，');
        return arr;
      }
      if(str.replace(/\s+/g,'').length == 0){
        return arr;
      }
      arr.push(str);
      return arr;
    }

上传文件

    function ajaxUploadFile(optsObj) {
      var fileObj = document.getElementById(optsObj.id).files[0]; // 获取文件对象
      var FileController = optsObj.url;     // 接收上传文件的后台地址
      // FormData 对象
      var form = new FormData();
      form.append("file", fileObj);         // 文件对象
      // XMLHttpRequest 对象
      var xhr = new XMLHttpRequest();
      xhr.open("post", FileController, true);
      xhr.setRequestHeader("token", storage.localStorage.get("token"));
      xhr.onload = function () {
        if (typeof(optsObj.success) == "function") {
          optsObj.success(eval('(' + this.responseText + ')'));
        }
      };
      xhr.send(form);
    }

exports utils  输出为utils

> ajax(options)

options为对象

    options = {
      contentType, // 默认为"application/json;charset=UTF-8"
      type, // 默认为 'post'
      async, // true为异步
      data,  // 请求的参数
      dataType, // 默认为 json
      beforeSend, // 请求前回调
      success:, // 请求成功后回调
      failure:, // 请求失败回调
      complete, // 请求完成回调
      error, // 请求错误回调
    }


> url

把参数放到url上面：url.set(params)

从url上获取参数： url.get(param)

住：若没有这个参数则返回null

> sobox

模态框

- `sobox.toast(content, time)`

`content`为显示的内容，`time`是显示的时长

- `sobox.alert(opts)`

`opts`是一个对象，对象内为：

`title`: '显示的标题' 默认为‘提示’

`content`: 显示的内容

`callback`: 回调函数

- `sobox.confirm(opts)`

`opts`是一个对象，对象内为：

`title`: '显示的标题' 默认为‘提示’

`content`: 显示的内容

`confirmCallback`: 确认回调函数

`cancelCallback`: 取消回调函数

> loading()

加载模态框，一般用于加载页面和ajax加载

> loaded()

移除加载模态框

> setPageTitle(title)

`string title` 设置页面显示标题，一般用于单页应用
