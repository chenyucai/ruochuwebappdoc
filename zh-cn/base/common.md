# 公共函数

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
