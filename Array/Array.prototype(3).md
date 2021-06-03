Array.prototype学习笔记(三)
=

## Array.prototype.forEach()
forEach()方法对数组的每个元素执行一次给定的函数.返回`undefined`  

### 语法
```
arr.forEach(callback(element[,index[,arr]])[,thisArg])
```

### 不对未初始化的值进行任何操作(稀疏数组)
```
let arraySparse = [1,3,,7];
let numCallbackRuns = 0;
arraySparse.forEach(function(element){
	console.log(element);
	numCallbackRuns++;
});
console.log("numCallbackRuns:",numCallbackRuns);
/*
1
3
7
numCallbackRuns: 3
*/
```

### 使用thisArg
```
function Counter(){
	this.sum = 0;
	this.count = 0;
}
Counter.prototype.add = function(array){
	array.forEach(function(entry){
		this.sum += entry;
		++this.count;
	},this)
};
let obj = new Counter();
obj.add([2,5,9]);
obj.count; //3 === (1 + 1 + 1)
obj.sum; //16 === (2 + 5 + 9)
```

### 数组迭代时被修改
```
let words = [1,2,3,4,5];
words.forEach(function(word){
	console.log(word);
	if(word === 2){
		words.shift();
	}
});
//1
//2
//4
//5
```

## Array.from()
Array.from()方法从一个类似数组或可迭代对象创建一个新的,浅拷贝的数组实例  
>类数组对象：拥有length属性的对象  
>可遍历对象：拥有Symbol.iterator接口的对象  

```
console.log(Array.from('foo'));//["f", "o", "o"]
console.log(Array.from([1,2,3],x => x+x)); //[2,4,6]
```

### 语法
```
Array.from(arrayLike[,mapFn[,thisArg]])
```
>arrayLike:想要转换成数组的伪数组对象或可迭代对象  
>mapFn可选，新数组中的每个元素会执行该回调函数  
>thisArg可选，执行回调函数mapFn时this对象  

### 从String生成数组
```
Array.from('foo');
//['f','o','o']
```

### 从Set生成数组
```
const set = new Set([1,2,3,4,5]);
Array.from(set);
//[1, 2, 3, 4, 5]
```

### 从Map生成数组
```
let map = new Map([[1,2],[3,4],[5,6]]);
Array.from(map);
//[[1,2],[3,4],[5,6]]

const mapper = new Map([['1','a'],['2','b']]);
Array.from(mapper.values()); //["a", "b"]
Array.from(mapper.keys()); //["1", "2"]
```

### 从类数组对象（arguments）生成数组
```
function f(){	
	return Array.from(arguments);
}
f(1,2,3); //[1, 2, 3]
```

### 在Array.from中使用箭头函数
```
Array.from([1,2,3],x => x*2); //[2, 4, 6]

Array.from({length:3},x => 1); //[1, 1, 1]
```

### 序列生成器（指定返回）
```
const range = (start, stop, step) => Array.from({length: (stop - start)/step + 1},(_, i) => start + (i * step));
range(0,4,1); //[0, 1, 2, 3, 4]

range('A'.charCodeAt(0), 'Z'.charCodeAt(0),1).map(x => String.fromCharCode(x));
//["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]
```

## Array.prototype.includes()
includes()方法用来判断一个数组是否包含一个指定的值，包含返回true,否则返回false  

### 语法
```
arr.includes(valueToFind[,fromIndex])
```

>如果fromIndex大于等于数组长度，返回false,且该数组不会被搜索  
>如果fromIndex为负值，fromIndex + arr.length < 0，整个数组都会被搜索

## Array.prototype.indexOf()
indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，返回-1  

### 语法
```
arr.indexOf(searchElement[,fromIndex])
```

## Array.isArray()
Array.isArray()用于确定传递的值是否是一个Array  

## Array.prototype.join()
join()将数组（类数组对象）的元素连接成一个字符串并返回这个字符串

```
arr.join([separator])
```

### 连接类数组对象
```
function f(a,b,c){
	var a = Array.prototype.join.call(arguments,'');
	console.log(a);
}
f(1,'a',true);  //1atrue
```












