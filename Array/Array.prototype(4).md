Array.prototype学习笔记(四)
=

## Array.prototype.keys()
keys()方法返回一个包含数组中每个索引键的Array Iterator对象  

### 语法
```
arr.keys()
```

```
let arr = ['a',,'c'];
let sparseKeys = Object.keys(arr);  //["0", "2"]
let denseKeys = [...arr.keys(arr)];  //[0, 1, 2]
```

## Array.prototype.lastIndexOf()
lastIndexOf()方法返回指定元素,在数组中的最后一个的索引,如果不存在返回-1.从数组的后面向前查找  

### 语法
```
arr.lastIndexOf(searchElement[,fromIndex])
```
>fromIndex若为负数,绝对值大于数组的长度,则返回-1,数组不会查找  

### 查找所有元素
```
var indices = [];
var array = ['a','b','a','c','a','d'];
var element = 'a';
var idx = array.lastIndexOf(element);

while(idx != -1){
	indices.push(idx);
	idx = (idx > 0 ? array.lastIndexOf(element,idx - 1) : -1);
}

console.log(indices);
```

## Array.prototype.map()
map()方法创建一个新数组,其结果是该数组中的每个元素是调用一次提供的函数后的返回值

### 语法
```
arr.map(callback(element[,index[,arr]])[,thisArg])
```

### 求数组中每个元素的平方根
```
var numbers = [1,4,9];
numbers.map(Math.sqrt); //[1,2,3]
```

### 使用map重新格式化数组中的对象
```
var kvArray = [{key:1,value:10},{key:2,value:20},{key:3,value:30}];

var reformattedArray = kvArray.map(function(obj){
	var rObj = {};
	rObj[obj.key] = obj.value;
	return rObj;
});
```

### 使用一个包含一个参数的函数来mapping一个数字数组
```
var numbers = [1,4,9];
var doubles = numbers.map(function(num){
	return num*2;
});  //[2, 8, 18]
```

### 一般map使用方法
```
var a = Array.prototype.map.call('Hello World',function(element){
	return element.charCodeAt(0);
});
a;//[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]
```

### querySelectorAll应用
```
var elems = document.querySelectorAll('select option:checked');
var values = Array.prototype.map.call(elems,obj => obj.value);
```

### parseInt
```
['1','2','3'].map(parseInt);  //[1, NaN, NaN]
/*
parseInt(value,index);
*/
```

### Mapping含undefined的数组
```
var numbers = [1,2,3,4];
var filteredNumbers = numbers.map((num,index) => {if(index<3){return nm;}});
filteredNumbers; //[1, 2, 3, undefined]
```

## Array.of()
Array.of()方法创建一个具有可变数量参数的新数组实例,而不考虑参数的数量或类型  
```
Array.of(7);  //[7]
Array.of(1,2,3); //[1,2,3]
Array.of(undefined); //[undefined]

Array(7);  //[,,,,,,]
Array(1,2,3); //[1,2,3]
```

## Array.prototype.pop()
pop()方法从数组中删除最后一个元素,并返回该元素的值.此方法更改数组的长度.  
pop 方法有意具有通用性。该方法和 call() 或 apply() 一起使用时，可应用在类似数组的对象上。pop方法根据 length属性来确定最后一个元素的位置。如果不包含length属性或length属性不能被转成一个数值，会将length置为0，并返回undefined。

### 返回值
从数组中删除的元素(数组为空时返回undefined)  

## Array.prototype.push()
push()方法将一个或多个元素添加到数组的末尾,并返回该数组的新长度  

push 方法具有通用性。该方法和 call() 或 apply() 一起使用时，可应用在类似数组的对象上。push 方法根据 length 属性来决定从哪里开始插入给定的值。如果 length 不能被转成一个数值，则插入的元素索引为 0，包括 length 不存在时。当 length 不存在时，将会创建它。
