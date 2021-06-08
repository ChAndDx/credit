Array.prototype学习笔记(五)
=

## Array.prototype.reduce()
reduce()方法对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值。  

### 语法
```
arr.reduce(callback(accumulator,currentValue[,index[,arr]])[,initialValue])
```
>`accumulator`累计器累计回调的返回值;它是上一次调用回调时返回的累积值,或initialValue  
>`currentValue`数组中正在处理的元素  
>`index`可选,数组中正在处理的当前元素的索引。如果提供了initialValue，则起始索引号为0，否则从索引1起始。  
>`arr`可选,调用reduce()的数组
>`initialValue`可选,作为第一次调用 callback函数时的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。  

### 数组里所有值的和
```
let sum = [1,2,3,4,5].reduce((accumulator,currentValue) => accumulator + currentValue,0);
```

### 累加对象数组里的值
```
[{a:1},{a:2},{a:3}].reduce((a,b)=>a+b.a,0);
```

### 将二维数组转化为一维
```
[[0,1],[2,3],[4,5]].reduce((a,b)=>a.concat(b),[]);
//[0, 1, 2, 3, 4, 5]
```

### 计算数组中每个元素出现的次数
```
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
names.reduce((allNames,name)=>{
if(name in allNames){
allNames[name]++;
}else{
allNames[name]=1;
}
return allNames;
},{});
```

### 按属性对object分类
```
var people = [
  { name: 'Alice', age: 21 },
  { name: 'Max', age: 20 },
  { name: 'Jane', age: 20 }
];

function groupBy(objectArray,property){
	return objectArray.reduce(function(acc,obj){
		let key = obj[property];
		if(!acc[key]){
			acc[key] = [];
		}
		acc[key].push(obj);
		return acc;
	},{});
}

var groupedPeople = groupBy(people, 'age');
// groupedPeople is:
// {
//   20: [
//     { name: 'Max', age: 20 },
//     { name: 'Jane', age: 20 }
//   ],
//   21: [{ name: 'Alice', age: 21 }]
// }
```

### 使用扩展运算符和initialValue绑定包含在对象数组中的数组
```
var friends = [{
  name: 'Anna',
  books: ['Bible', 'Harry Potter'],
  age: 21
}, {
  name: 'Bob',
  books: ['War and peace', 'Romeo and Juliet'],
  age: 26
}, {
  name: 'Alice',
  books: ['The Lord of the Rings', 'The Shining'],
  age: 18
}];

var allbooks = friends.reduce(function(prev,curr){
	return [...prev,...curr.books];
}, ['Alphabet']);
```

### 数组去重
```
let orderedArray = Array.from(new Set(myArray));
```

```
let myArray = ['a', 'b', 'a', 'b', 'c', 'e', 'e', 'c', 'd', 'd', 'd', 'd']
let myOrderedArray = myArray.reduce(function (accumulator, currentValue) {
  if (accumulator.indexOf(currentValue) === -1) {
    accumulator.push(currentValue)
  }
  return accumulator
}, [])

console.log(myOrderedArray)
```

```
let arr = [1,2,1,2,3,5,4,5,3,4,4,4,4];
let result = arr.sort().reduce((init, current) => {
    if(init.length === 0 || init[init.length-1] !== current) {
        init.push(current);
    }
    return init;
}, []);
console.log(result); //[1,2,3,4,5]
```

### 按顺序运行Promise
```
function runPromiseInSequence(arr, input) {
  return arr.reduce(
    (promiseChain, currentFunction) => promiseChain.then(currentFunction),
    Promise.resolve(input)
  );
}

// promise function 1
function p1(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 5);
  });
}

// promise function 2
function p2(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 2);
  });
}

// function 3  - will be wrapped in a resolved promise by .then()
function f3(a) {
 return a * 3;
}

// promise function 4
function p4(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 4);
  });
}

const promiseArr = [p1, p2, f3, p4];
runPromiseInSequence(promiseArr, 10)
  .then(console.log);   // 1200
```

### 功能型函数管道
```
// Building-blocks to use for composition
const double = x => x + x;
const triple = x => 3 * x;
const quadruple = x => 4 * x;

// Function composition enabling pipe functionality
const pipe = (...functions) => input => functions.reduce(
    (acc, fn) => fn(acc),
    input
);

// Composed functions for multiplication of specific values
const multiply6 = pipe(double, triple);
const multiply9 = pipe(triple, triple);
const multiply16 = pipe(quadruple, quadruple);
const multiply24 = pipe(double, triple, quadruple);

// Usage
multiply6(6); // 36
multiply9(9); // 81
multiply16(16); // 256
multiply24(10); // 240
```

### 使用 reduce实现map
```
if (!Array.prototype.mapUsingReduce) {
  Array.prototype.mapUsingReduce = function(callback, thisArg) {
    return this.reduce(function(mappedArray, currentValue, index, array) {
      mappedArray[index] = callback.call(thisArg, currentValue, index, array)
      return mappedArray
    }, [])
  }
}

[1, 2, , 3].mapUsingReduce(
  (currentValue, index, array) => currentValue + index + array.length
) // [5, 7, , 10]
```


















## Array.prototype.reduceRight()