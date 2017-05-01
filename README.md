##WxTouchEvent 微信小程序手势事件库

由于微信小程序只能够支持 tap,longtap,touchstart,touchmove,touchcancel,touchend时间，对于比较复杂的事件只能自己实现
因此自己对 `alloyFinger`库进行了改造，开发了时候微信小程序手势事件库`WxTouchEvent`,使用 ES
6进行编写,手势库支持以下事件

*   touchStart
*   touchMove
*   touchEnd
*   touchCancel
*   multipointStart
*   multipointEnd
*   tap
*   doubleTap
*   longTap
*   singleTap
*   rotate
*   pinch
*   pressMove
*   swipe


###使用
由于和微信小程序强绑定，因此需要在元素上面绑定好所有的事件，书写比较麻烦，因此建议对于原生支持的使用原生去解决，
只有当需要 pinch，rotate,swipe 等特殊事件才使用这个事件库实现

> 安装 `npm i wx-touch-event --save` , 或者直接从 git 库 checkout 出来 

绑定方法
#### \*.wxml
在`wxml`中对需要监听时间的元素绑定 `touchstart、touchmove、touchend、touchcancel`四个事件
页面书写成

``` 
    <view class="info-list" 
          bindtouchstart="touchStart"
          bindtouchmove="touchMove"
          bindtouchend="touchEnd"
          bindtouchcancel="touchCancel"
        >
        
    </view>
```

#### \*.js
在`js`逻辑层需要实例化`WxTouchEvent`, 实例中有`start、move、end、cancel`对应`\*.wxml`绑定的`bindtouchstart,bindtouchmove,bindtouchend,bindtouchcancel`,需要将事件的回调函数一一对应,
书写成:

```
import WxTouchEvent from "wx-touch-event";

let infoListTouchEvent = new WxTouchEvent();//在 Page外实例化函数，可以直接复制给 Page 中的回调函数
Page({
    onLoad: function() {
        this.infoListTouchEvent = infoListTouchEvent;
        this.infoListTouchEvent.bind({//初始化后绑定事件
            swipe: function(e) {
                console.log(e);
            },
            doubleTap: function(e) {
                console.log(e);
            },
            tap: function(e) {
                console.log(e);
            }.bind(this),
            longTap: function(e) {
                console.log(e);
            },
            rotate: function(e) {
                console.log(e)
            }.bind(this),
            pinch: function(e) {
                console.log(e);
            }

        })
    },
    touchStart: infoListTouchEvent.start.bind(infoListTouchEvent),
    touchMove: infoListTouchEvent.move.bind(infoListTouchEvent),
    touchEnd: infoListTouchEvent.end.bind(infoListTouchEvent),
    touchCancel: infoListTouchEvent.cancel.bind(infoListTouchEvent),

});
```



