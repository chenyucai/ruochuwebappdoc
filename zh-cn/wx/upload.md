> 上传图片api

    chooseImgs: function(e){
      var _this = this;
      var $el = $(e.currentTarget);
      wx.ready(function(){
        wx.chooseImage({
          success: function(res){
            var localIds = res.localIds;
            function uploadImg(ids, _i){
              _this.loading.show = true;
              var i = _i;
              wx.uploadImage({
                localId: ids[i],
                isShowProgressTips: 0, // 默认为1，显示进度提示
                success: function(res){
                  var serverId = res.serverId;
                  $.ajax({
                    url:  '/api/client/wxUpload',
                    contentType:"application/x-www-form-urlencoded; charset=UTF-8",
                    type:"post",
                    dataType:"json",
                    headers:{token:token},
                    data: {mediaId: serverId},
                    complete: function(){
                      _this.loading.show = false;
                    },
                    success: function(response){
                      var url = response.rs.url;
                      _this.resInfo.checkImgs.push(url);
                    }
                  });
                  i++;
                  if (i < ids.length) {
                    uploadImg(ids,i);
                  }
                }
              });
            }
            uploadImg(localIds, 0);
          }
        });
      });
    }
