Wechat Push
=============
使用方式如下：

```
var Pusher = require('wechat_push');

var handleMessage = function(message){
  console.log((new Date()) * 1);
}

var handleError = function (error) {
  console.log(error);
}

var p = new Pusher('username', 'password');

p.login(function(err, verify){  // A callback for login is required
  if (err) { 
    console.log(err);
  }
  if (verify) {  // need verify code
    console.log(verify);
    // `verify` is alias `p.err`
  }
  // otherwise, login success;

  p.on('message', handleMessage);
  p.on('error', handleError);

  p.send('177366',  // Fromfakeid, your own fakeId 
         '177366',  // Tofakeid
         'message', // message
         function(err, body){
           if (err )
             return console.log(err);
           // if success, a fetch worker will start and
           // you are able to listen on `err` for handling 
           // fetch err and `message` for handling new message
           // Known bug:
           // If use send, the worker will not work
           // because the raw cookie was modified when referenced
           // So a copy of cookie is necessary
           console.log(body);
         });
});
```

## 注意
由于微信方面没有公开相关API，不能保证本模块能永远正常工作。

## License
The MIT License

## 捐赠
如果您觉得本模块对您有帮助，欢迎请作者一杯咖啡：

[![捐赠Wechat Push](https://img.alipay.com/sys/personalprod/style/mc/btn-index.png)](https://me.alipay.com/jacksontian)
