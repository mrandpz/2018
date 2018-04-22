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

`'+new Array(017)'`

`输出？（ ）`

首先，前面+是一元运算符，相当于我们说的正负，无运算效果，但是可以将字符串等转为number类型。

此题中017其实是八进制，故而是是Array\(15\)。

这里相当于对于一个未赋值但是长度为15的数组进行number类型转化，其结果为NaN

3.如何判断一个js对象是否是Array,arr为要判断的对象，其中最准确的方法是？

```
Obkect.prototype.toString.call(arr) === '[Object Array]'
```

4.![](/assets/import.png)

输出结果为 4400 4401 4399 4400

因为result 和result2 返回的是不同的对象，互不影响， result.n result2.n 的指向都是不相同的

5.假设val已经声明,可定义为任何值。则下面js代码有可能输出的结果为:

```
console.log('Value is ' + (val != '0') ? 'define' : 'undefine');
```

加号优先级高于 三目运算。低于括号。 所以括号中无论真假 加上前边的字符串都为 TRUE 三目运算为TRUE是 输出 define

6. setTimeout 并不是全局函数

![](/assets/全局函数.png)























