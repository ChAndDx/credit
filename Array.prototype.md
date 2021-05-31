Array.prototype学习笔记
=
Array.prototype.concat
-
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