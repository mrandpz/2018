1. Lazy\_Man：队列，工厂模式，闭包，异步，链式

Lazy\_Man\('榕'\).rest\(5\).eat\('面线糊'\)

Lazy\_Man\('榕'\).restFirst\(5\).eat\('面线糊'\)

```
function _LazyMan(name) {
    this.tasks = [];   
    var self = this;
    var fn =(function(n){
        var name = n;
        return function(){
            console.log("Hi! This is " + name + "!");
            self.next();
        }
    })(name);
    this.tasks.push(fn);
    setTimeout(function(){
        self.next();
    }, 0); // 在下一个事件循环启动任务
}
/* 事件调度函数 */
_LazyMan.prototype.next = function() { 
    var fn = this.tasks.shift();
    fn && fn();
}
_LazyMan.prototype.eat = function(name) {
    var self = this;
    var fn =(function(name){
        return function(){
            console.log("Eat " + name + "~");
            self.next()
        }
    })(name);
    this.tasks.push(fn);
    return this; // 实现链式调用
}
_LazyMan.prototype.sleep = function(time) {
    var self = this;
    var fn = (function(time){
        return function() {
            setTimeout(function(){
                console.log("Wake up after " + time + "s!");
                self.next();
            }, time * 1000);
        }
    })(time);
    this.tasks.push(fn);
   return this;
}
_LazyMan.prototype.sleepFirst = function(time) {
    var self = this;
    var fn = (function(time) {
        return function() {
            setTimeout(function() {
                console.log("Wake up after " + time + "s!");
                self.next();
            }, time * 1000);
        }
    })(time);
    this.tasks.unshift(fn);
    return this;
}
/* 封装 */
function LazyMan(name){
    return new _LazyMan(name);
}
LazyMan('jack')

2.jquery ajax中都支持哪些数据类型？
通过dataType选项还可以指定其他不同数据处理方式。除了单纯的XML，还可以指定 html、json、jsonp、script或者text。

3.常见的浏览器端的存储技术有哪些
```

有时需要将网页中的一些数据保存在浏览器端，这样做的好处是，当下次访问页面时，不需要再次向服务器请求数据，直接就可以从本地读取数据。目前常用的有以下几种方法：

**cookie**

cookie会随着每次HTTP请求头信息一起发送，无形中增加了网络流量，另外，cookie能存储的数据容量有限，根据浏览器类型不同而不同，IE6大约只能存储2K。

**Flash ShareObject**

这种方式能能解决上面提到的cookie存储的两个弊端，而且能够跨浏览器，应该说是目前最好的本地存储方案。不过，需要在页面中插入一个Flash，当浏览器没有安装Flash控件时就不能用了。所幸的是，没有安装Flash的用户极少。

缺点：需要安装Flash插件。

**Google Gear**

Google开发出的一种本地存储技术。

缺点：需要安装Gear组件。

**userData**

IE浏览器可以使用userData来存储数据，容量可达到640K，这种方案是很可靠的，不需要安装额外的插件。缺点：它仅在IE下有效。

**sessionStorage**

使用于Firefox2+的火狐浏览器，用这种方式存储的数据仅窗口级别有效，同一个窗口（或者Tab）页面刷新或者跳转，都能获取到本地存储的数据，当新开窗口或者页面时，原来的数据就失效了。

缺点：IE不支持、不能实现数据的持久保存。

**globalStorage**

使用于Firefox2+的火狐浏览器，类似于IE的userData。

缺点：IE不支持。

**localStorage**

localStorage是Web Storage互联网存储规范中的一部分，现在在Firefox 3.5、Safari 4和IE8中得到支持。

缺点：低版本浏览器不支持。

结论：  
Flash shareobject是不错的选择，如果你不想在页面上嵌入Flash，可以结合使用userData\(IE6+\)和globalStorage\(Firefox2+\)和localStorage\(chrome3+\)实现跨浏览器。

4.

js七种数据类型：Sting  Object  null  undefined  Array  Boolean  Number

js五种基本类型：String Boolean Number null undefined

typeof六种返回格式：'string'  'number'  'object'  'function'  'boolean'  'undefined'

5.请给Array本地对象增加一个原型方法，它用于删除数组条目中重复的条目\(可能有多个\)，返回值是一个包含被删除的重复条目的新数组。

```
Array.prototype.distinct = function() {
    var ret = [];
    for (var i = 0; i < this.length; i++){
        for (var j = i+1; j < this.length;) {   
            if (this[i] === this[j]) {
                ret.push(this.splice(j, 1)[0]); 
// 因为splice返回的是包含删除元素的数组,加个[0]把删除的元素取出来，然后push到ret中  
//slice方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。
            } else {
                j++;
            }
        }
     }
     return ret;
}
//for test
console.log([2,2,23,4,5,3,2,32,5,5,5].distinct());
```





