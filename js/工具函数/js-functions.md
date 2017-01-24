# JS 工具类函数

#### 判断是不是微信浏览器
>如何判断微信内置浏览器，首先需要获取微信内置浏览器的User Agent，经过在 iPhone 上微信的浏览器的检测，
它的 User Agent 是：
~~~
Mozilla/5.0 (iPhone; CPU iPhone OS 6_1_3 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Mobile/10B329 MicroMessenger/5.0.1
~~~
>所以通过识别 MicroMessenger 这个关键字来确定是否微信内置的浏览器了。
~~~
function is_weixin(){
    var ua = navigator.userAgent.toLowerCase();
    if(ua.match(/MicroMessenger/i)=="micromessenger") {
        return true;
    } else {
        return false;
    }
}
~~~