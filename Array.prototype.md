Array.prototype学习笔记
=

Array.prototype.concat
-

concat()方法用于合并两个或多个数组。  

```
let arr1 = '123',
    arr2 = '456';
let arr = arr1.concat(arr2);
arr; //"123456"
```

```
let arr1 = '123';
let arr = arr1.concat(4,[5],[[6]]);
arr; //"123456"
```


Array.prototype.copyWithin()
-

copyWithin()方法浅复制数组的一部分到同一数组中的另一个位置，不会改变数组的长度  

语法：
```
arr.copyWithin(target[,start[,end]])
```
target:复制序列到该位置  
start:复制元素的起始位置  
end:拷贝到该位置但不包括end
```
let arr = ['a','b','c','d','e','f','g'];
arr.copyWithin(1,0,2);
arr;  //['a','a','b','d','e','f','g']
```

Array.prototype.entries()
-

entries()方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对  
### Array Iterator
```
let arr = ['a','b','c'];
let iterator = arr.entries();
console.log(iterator);
/*Array Iterator {}
    __proto__: Array Iterator
    next: ƒ next()
    Symbol(Symbol.toStringTag): "Array Iterator"
    __proto__: Object
*/
```

### iterator next()
```
let arr = ['a','b','c'];
let iterator = arr.entries();
console.log(iterator.next());
/*{value: Array(2), done: false}
    done: false
    value: (2) [0, "a"]
    __proto__: Object
*/
//next.done用于指示迭代器是否完成，每次迭代时进行更新而且都是false,直到迭代器结束时，done为true
```

### iterator.next方法运行
```
let arr = ['a','b','c'];
let a = [];
let entries = arr.entries();
for(let i = 0; i < arr.length; i++){
    var tem = entries.next();
    if(tem.done != true){
        a.push(tem.value);
    }
}
console.log(a);
/*[Array(2), Array(2), Array(2)]
0: (2) [0, "a"]
1: (2) [1, "b"]
2: (2) [2, "c"]
length: 3
__proto__: Array(0)
*/
```

### 二维数组排序
```
function sortArr(arr){
    for(let e of arr.entries()){
        e[1].sort((a,b)=>a-b)
    }
    return arr;
}
let arr = [[2,4,1,5,4],[2,1]];
sortArr(arr);
```

### for of
```
let arr = ['a','b','c'];
for(let e of arr.entries()){
    console.log(e)
}
/*(2) [0, "a"]
(2) [1, "b"]
(2) [2, "c"]
*/
```
