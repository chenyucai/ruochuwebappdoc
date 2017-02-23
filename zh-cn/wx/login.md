> 微信授权登录

    <script type="text/javascript">
        function getUrlParameter(params, paramName){
          var reg = new RegExp("(^|&)"+ paramName +"=([^&]*)(&|$)");
          var r = params.substr(1).match(reg);
          if(r!=null) return  unescape(r[2]); return "";
        }

        var state = getUrlParameter(param, "state");
        var url = "https://open.weixin.qq.com/connect/oauth2/authorize?appid="+appid+
        "&redirect_uri=http://"+appid+".wx.ruochuchina.com/api/client/wxoauth2&
        response_type=code&scope=snsapi_base&state=" + state +
        "&component_appid=wx09882bcaadbbbd8d#wechat_redirect";

        window.location.href = url;
    </script>
