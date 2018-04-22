1.插入排序

```
function insetSort(arr) {
  var i,j,tmp,len=arr.length,result;
  result = arr.slice(0);
  for(i=1;i<len;i++){
    tmp = result[i];
    j = i-1;
    // 当tmp = -1 j=3 i=4 此时 tmp<result[j]为(1) 满足条件,将-1这个插槽换成5，j为2，再继续对比发现还是比3小
    // 继续对比直到 j=0 result[0]=1;还是比-1大，所以j继续-1等于-1时跳出循环。
    // result[0] = -1
    while(j>=0 && tmp < result[j]){
      result[j+1] = result[j];
      j--;
    }
    result[j+1] = tmp
  }
}
insetSort([1,1,3,5,-1])
```

**基本思想:**

将一个记录插入到已排序好的有序表中，从而得到一个新，记录数增1的有序表。即：先将序列的第1个记录看成是一个有序的子序列，然后从第2个记录逐个进行插入，直至整个序列有序为止。

**优点:**稳定，快

**缺点：**比较次数不一定，比较次数越少，插入点后的数据移动越多，特别是当数据总量庞大的时候

