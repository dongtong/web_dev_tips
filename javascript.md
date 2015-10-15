1. jQuery Ajax回调执行函数执行顺序

        ajaxStart(全局事件) -> beforeSend -> ajaxSend(全局事件) -> success -> ajaxSuccess(全局事件) ->
        error -> ajaxError (全局事件) -> complete -> ajaxComplete(全局事件) -> ajaxStop(全局事件)
  
  error出现的错误，在complete中依旧能捕捉到，如果想在complete中捕捉timeout错误，那么在error中可以不考虑timeout错误。
  
2. jsonp跨域请求

  在调用jsonp请求接口时最好指定jsonpCallback参数，即使服务端正常返回200，但是如果ajax指定了error回调，也会报error错误
  
        $.ajax({
          type: "GET",
          url: options.url,
          data: options.data || null, //"{}"
          cache: false,
          timeout: Const.TIME_OUT,
          crossDomain: true,
          dataType: "jsonp",
          jsonpCallback: options.jsonpCallback || null,
          contentType: "application/json;utf-8", 
          success: function(){},
          error: function(){
            //如果不指定jsonpCallback参数，那么会走到这里
          }
        });
