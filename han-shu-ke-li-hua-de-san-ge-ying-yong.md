摘抄 [https://mp.weixin.qq.com/s/jd5xVj-ajDLtdCaJwJFTdw](https://mp.weixin.qq.com/s/jd5xVj-ajDLtdCaJwJFTdw "函数柯里化")

1. 兼容浏览器事件监听方法

```js
var addEven = function (ele,type,fn,isCapture) {
    if (window.addEventListener) {
        ele.addEventListener(type,fn,isCapture)
    }else if(window.attachEvent){
        ele.attachEvent("on"+type,fn)
    }
}

// best
var addEven = (function (ele,type,fn,isCapture) {
    if (window.addEventListener) {
        return function(ele, type, fn, isCapture) {
            ele.addEventListener(type, fn, isCapture)
        }
    }else if(window.attachEvent){
        return function(ele, type, fn) {
             ele.attachEvent("on" + type, fn)
        }
    }
})()
```

这个例子利用了柯里化提前返回和延迟执行的特点，如下：

* 提前返回 – 使用函数立即调用进行了一次兼容判断（部分求值），返回兼容的事件绑定方法

* 延迟执行 – 返回新函数，在新函数调用兼容的事件方法。等待`addEvent`新函数调用，延迟执行

这就是柯里化函数的基本用法 – 提前返回**和**延迟执行，但是这里没有利用到柯里化参数复用的特点，接下来我们继续分析防抖和节流。

1. 防抖和节流，在scoll，resize，mousemove 事件中

##### 防抖（Debouncing）

```
/*
* @param    fn              Function    事件处理函数
* @param    delay           Number      延迟时间
* @param    isImmediate     Boolean     是否滚动时立刻执行
* @return   Function                    事件处理函数
*/
var debounce = function(fn, delay, isImmediate) {
    //使用闭包，保存执行状态，控制函数调用顺序
    var timer;

    return function() {
        var _args = [].slice.call(arguments),
            context = this;

        clearTimeout(timer);

        var _fn = function() {
            timer = null;
            if (!isImmediate) fn.apply(context, _args);
        };

        //是否滚动时立刻执行
        var callNow = !timer && isImmediate;

        timer = setTimeout(_fn, delay);

        if(callNow) fn.apply(context, _args);
    }
}
var debounceScroll = debounce(function() {
    //事件处理函数，滚动时进行的处理
}, 100)
window.addEventListener("scroll", debounceScroll)
```

防抖技术仅靠传入延迟时间值的大小控制高频事件的触发频率，如果传入的延迟时间值比较大，那么就会出现一定的问题。例如当传入延迟时间为1000ms，那么当用户滚动速度大于1000ms/次时，则无论鼠标滚动多久都不会触发事件处理函数。因此防抖技术存在一定的缺陷，会不适用于某些场景，例如图片懒加载。这个时候节流就派上用场了。

##### 节流（Throttle）

节流实现原理跟防抖技术类似，但是比防抖多了一次函数执行判断，实现的关键点是：

* 利用闭包存储了当前和上一次执行的时间戳，通过两次函数执行的时间差跟指定的延迟时间的比较，控制函数是否立刻执行

```
/*
* @param    fn          Function    事件处理函数
* @param    wait        Number      延迟时间
* @return   Function                事件处理函数
*/
var throttle = function(fn, wait) {
    var timer, previous, now, diff;
    return function() {
        var _args = [].slice.call(arguments),
            context = this;
        //储存当前时间戳
        now = Date.now();

        var _fn = function() {
            //存储上一次执行的时间戳
            previous = Date.now();
            timer = null;
            fn.apply(context, _args)
        }

        clearTimeout(timer)

        if(previous !== undefined) {
            //时间差
            diff = now - previous;
            if(diff >= wait) {
                fn.apply(context, _args);
                previous = now;
            } else {
                timer = setTimeout(_fn, wait);
            }
        }else{
            _fn();
        }
    }
}
```



