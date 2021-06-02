Array.prototype学习笔记(二)
=

## Array.prototype.filter()


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
let arr = [10,9,13,5,13];
function isBigEnough(element){
    return element >= 10;
}
arr.filter(isBigEnough); //[10, 13, 13]
```

### 过滤JSON中的无效头目
创建具有非零id的元素的json
```
var arr = [
    {id : 12},
    {id : -1},
    {id : 0},
    {id : NaN},
    {id : 'undefined'},
    {id : null},
    {id : 12.3},
    {},
    {id : 3},
];
function isNumber(obj){
    return obj !== undefined && typeof(obj) === 'number' && !isNaN(obj);
}
function filterById(element){
    if(isNumber(element.id) && element.id !== 0){
        return true;
    }
    return false;
}
arr.filter(filterById);

/*[{…}, {…}, {…}, {…}]
0: {id: 12}
1: {id: -1}
2: {id: 12.3}
3: {id: 3}
*/
```

## Array.prototype.find()
find()方法返回数组中满足提供的测试函数的第一个元素的值。否则返回`undefined`  

### 语法
```
arr.find(callback(element[,index[,array]])[,thisArg])
```

### 返回值
返回数组中第一个满足所提供测试函数的元素的值，否则返回`undefined`  

### 寻找数组中的质数
```判断是否为质数
function isPrime(element){
    let start = 2;
    while(start <= Math.sqrt(element)){
        if(element % start++ < 1){
            return false;
        }
    }
    return element > 1;
}
```
### `ps`:当回调中删除数组中的一个值时，当访问到这个位置时，其传入的值是`undefined`

## Array.prototype.findIndex()
返回数组中满足提供的测试函数的第一个元素的`索引`。若没有找到对应元素则返回`-1`  

## Array.prototype.flat()
flat()方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组的元素合并为一个新数组返回

### 语法
```
var newArray = arr.flat([depth])
```
>depth:可选，指定要提取嵌套数组的结构深度，默认值为1。  
返回一个包含将数组与子数组中所有元素的新数组  

### 扁平化嵌套数组
```
let arr1 = [1,2,[3,4]];
arr1.flat(); //[1,2,3,4]

let arr2 = [1,2,[3,4,[5,6]]];
arr2.flat(); //[1,2,3,4,[5,6]]
arr2.flat(2);//[1,2,3,4,5,6]

//使用Infinity,可以展开任意深度的嵌套数组
```

### 扁平化与数组空项
flat()会移除数组中的空项
```
let arr = [1,,2,3];
arr.flat();//[1, 2, 3]
```

## Array.prototype.flatMap()
flatMap()方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。它与map连着深度为1的flat几乎相同，但flatMap通常在合并成一种方法的效率稍微高一些。

### 语法
```
let newArray = arr.flatMap(callback(element[,index[,arr]])[,thisArg])
```
返回一个新的数组，其中每个元素都是回调函数的结果，并且结构深度depth值为1  

### map()与flatMap()
```
let arr1 = [1,2,3,4];
arr1.map(x => [x*2]); //[[2],[4],[6],[8]]
arr1.flatMap(x => [x*2]); //[2,4,6,8]
arr1.flatMap(x => [[x*2]]); //[[2],[4],[6],[8]]
```

```
let arr2 = ['it is','','cat'];
arr2.map(x => x.split(" "));
/*[Array(2), Array(1), Array(1)]
0: (2) ["it", "is"]
1: [""]
2: ["cat"]
length: 3
__proto__: Array(0)
*/

arr2.flatMap(x => x.split(" ")); //["it", "is", "", "cat"]
```