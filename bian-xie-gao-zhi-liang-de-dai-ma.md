意识到的bug及时修复，当你发现bug 的时候就立即修复它是最好的。不然随着时间的流逝，新功能的添加，重新阅读代码或者别人介入阅读代码的成本很大，阅读代码花费的时间会比编辑代码的时间多很多。

1. 不使用全局变量，使用全局变量会影响到第三方插件，并且在所有的代码中，都共享这个全局变量，造成内存损耗。
2. 单var 形式，提供了一个单一的地方去寻找功能所需要的所有局部变量，少代码。
   ```
   function func() {
      var a = 1,
          b = 2,
          sum = a + b,
          myobject = {},
          i,
          j;
      // function body...
   }
   ```
3. for循环   提取max
   ```
   function looper() {
      var i = 0,
           max,
           myarray = [];
      // ...
      for (i = 0, max = myarray.length; i < max; i++) {
         // 使用myarray[i]做点什么
      }
   }
   ```
4. 不扩展内置原型。  Array.prototypr.someMehtods = function\(\){}  除非：使用率很大，与所有开发人员沟通好，定义前检查是否已存在
   ```
   if (typeof Object.protoype.myMethod !== "function") {
      Object.protoype.myMethod = function () {
         // 实现...
      };
   }
   ```
5. 使用 === 不使用 ==  避免隐式转换
6. parseInt\('10',10\)  增加10进制数字
7. 缩进与空格： 使用一个tab两个空格的eslint，并且在英文字符的前后加上空格增加可阅读性。
8. for if等后面的花括号不省略，return后面的花括号不能换行
9. 全局变量名字全部大写，私有变量用下划线 \_
   ```
   _getLast: function () {
           // ...
       }
   ```
10. 注释，尽量详细，虽然自己看得懂，但是过段时间，或者别人来阅读的时候，就要花费更多时间



