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
    alert(a); //undefined
    alert(b); //undefined
    b=3;  // b是全局变量
    alert(a); //undefined
    alert(b);  // 3
})();
alert(a); //undefined，undefined
alert(b); //undefined
```

2.

`'+new Array(017)'`

`输出？（ ）`

首先，前面+是一元运算符，相当于我们说的正负，无运算效果，但是可以将字符串等转为number类型。  

 此题中017其实是八进制，故而是是Array\(15\)。  

这里相当于对于一个未赋值但是长度为15的数组进行number类型转化，其结果为NaN

3.如何判断一个js对象是否是Array,arr为要判断的对象，其中最准确的方法是？

```
Obkect.prototype.toString.call(arr) === '[Object Array]'
```



