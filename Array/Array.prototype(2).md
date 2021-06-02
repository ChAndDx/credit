Array.prototype学习笔记(二)
=

Array.prototype.filter()
-

filter()方法创建一个新数组,其包含通过所提供函数实现的测试的所有元素  

### 语法
```
var newArray = arr.filter(callback(element[,index[,array]]),[,thisArg])
```
>`callback`用来判断数组的每个元素的函数.返回true表示该元素通过判断,保留元素  
>`element`数组中当前正在处理的元素
>`index`正在处理的元素在数组中的索引
>`array`调用filter的数组本身
>`thisArg`执行callback时,用于this的值  

### 筛选排除所有较小的值
```

```