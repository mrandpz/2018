1.插入排序

```
	function insertSort(array) {
	  var len = array.length,
	      i, j, tmp, result;
	  result = array.slice(0);
	  for(i=1; i < len; i++){
	    tmp = result[i]; 
	    j = i - 1; 
	    while(j>=0 && tmp < result[j]){
	      result[j+1] = result[j];
	      j--;
	    }
	    result[j+1] = tmp;
	  }
	  return result;
	}
```

**基本思想:**

将一个记录插入到已排序好的有序表中，从而得到一个新，记录数增1的有序表。即：先将序列的第1个记录看成是一个有序的子序列，然后从第2个记录逐个进行插入，直至整个序列有序为止。

**优点:**稳定，快

**缺点：**比较次数不一定，比较次数越少，插入点后的数据移动越多，特别是当数据总量庞大的时候



