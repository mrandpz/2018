1.

```
var a,b;
(function(){
    alert(a);
    alert(b);
    var a=b=3;
    alert(a);
    alert(b);
})();
alert(a);
alert(b);
```

相当于

```
var a,b;
(function(){
    var a = b;
    alert(a);
    alert(b);
    b=3;  // b是全局变量
    alert(a);
    alert(b);
})();
alert(a);
alert(b);
```



