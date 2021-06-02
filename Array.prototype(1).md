Array.prototype学习笔记(-)
=

Array.prototype.concat()
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

Array.prototype.every()
-

every()方法测试一个数组内的所有元素是否都能通过某个指定函数的测试,返回布尔值  
`收到空数组,一切情况下都返回true`  

### 语法
```
arr.every(callback(element[,index[,array]])[,thisArg])
```

>`callback`用来测试每个元素的函数,可以接收三个参数
>`element`用于测试的当前值
>`index`可选,用于测试的当前值的索引
>`array`可选,调用every的当前数组
>`thisArg`执行callback时使用的this值  

### 检测所有元素的大小
```
function isBigEnough(element,index,array){
	return element >= 10;
}
[12,5,11,13].every(isBigEnough); //false
[12,11,10,13,15].every(isBigEnough); //true
```

#### 使用箭头函数
```
[12,5,11,13].every(x => x>=10); //false
[12,11,10,13,15].every(x => x>= 10); //true
```

Array.prototype.fill()
-

fill()方法用于一个固定值填充一个数组中\[起始索引,终止索引\)内的元素.返回修改后的数组  

```
[1,2,3].fill(4);    //[4,4,4]
[1,2,3].fill(4,1);  //[1,4,4]
[1,2,3].fill(4,NaN,NaN); //[1,2,3]
Array(3).fill(4);   //[4,4,4]
[].fill.call({length:3},4);  //{0:4,1:4,2:4,length:3}

var arr = Array(3).fill({})  //[{},{},{}]
//fill的参数为引用类型,会导致都执行一个引用类型
//如arr[0] === arr[1] 为true
arr[0].hi = 'hi';  //[{hi: "hi"},{hi: "hi"},{hi: "hi"}]
```
