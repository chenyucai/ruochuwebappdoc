> 分享接口 `shareApp(opts)`

    function shareApp(options){
      wx.ready(function(){
        wx.onMenuShareTimeline({
          title: options.title, // 分享标题
          link: options.link, // 分享链接
          imgUrl: options.imgUrl, // 分享图标
          success: function () {
              // 用户确认分享后执行的回调函数
          },
          cancel: function () {
              // 用户取消分享后执行的回调函数
          }
        });
        wx.onMenuShareAppMessage({
          title: options.title, // 分享标题
          desc: options.desc, // 分享描述
          link: options.link, // 分享链接
          imgUrl: options.imgUrl, // 分享图标
          type: '', // 分享类型,music、video或link，不填默认为link
          dataUrl: '', // 如果type是music或video，则要提供数据链接，默认为空
          success: function () {
              // 用户确认分享后执行的回调函数
          },
          cancel: function () {
              // 用户取消分享后执行的回调函数
          }
        });
      });
    }
