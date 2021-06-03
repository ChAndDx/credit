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

```












