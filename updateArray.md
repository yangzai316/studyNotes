# ES6对数组的扩展
### 1、扩展运算符
将一个数组转为用逗号分隔的参数序列。<br>
主要用于函数调用。<br>
```javascript
function push(array, ...items) {
  array.push(...items);
}
```
如果扩展运算符后面是一个空数组，则不产生任何效果。<br>
### 2、Array.from()
将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）<br>
### 3、Array.of()
方法用于将一组值，转换为数组。
```javascript
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```
### 4、数组实例 copyWithin()
在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
接受三个参数：
	target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
	start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
	end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
这三个参数都应该是数值，如果不是，会自动转为数值。

// 将3号位复制到0号位
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
// [4, 2, 3, 4, 5]
```
### 5、数组实例 find() 和 findIndex()
数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。<br>
```javascript
find方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```
数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。
```javascript
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```
这两个方法都可以接受第二个参数，用来绑定回调函数的this对象。<br>
这两个方法都可以发现NaN，弥补了数组的indexOf方法的不足。
```javascript
[NaN].indexOf(NaN)
// -1
[NaN].findIndex(y => Object.is(NaN, y))
// 0
indexOf方法无法识别数组的 NaN 成员，但是findIndex方法可以借助Object.is方法做到。
```
### 6、数组实例 fill()
fill方法使用给定值，填充一个数组。<br>
fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]

['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```
### 7、数组实例 entries()，keys() 和 values()
entries()，keys()和values()————用于遍历数组。它们都返回一个遍历器对象，可以用for...of循环进行遍历；<br>
唯一的区别是：<br>
	keys()是对键名的遍历<br>
	values()是对键值的遍历<br>
	entries()是对键值对的遍历。
```javascript
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
### 8、数组实例 includes()
返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。
该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。
```javascript
[1, 2, 3].includes(2)     // true
```
indexOf方法有两个缺点：<br>
一是不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于-1，表达起来不够直观；<br>
二是，它内部使用严格相等运算符（===）进行判断，这会导致对NaN的误判。
### 9、数组实例 flat()，flatMap()
数组的成员有时还是数组，flat()用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数据没有影响。
```javascript
[1, 2, [3, 4]].flat()
// [1, 2, 3, 4]
```
flat()默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将flat()方法的参数写成一个整数，表示想要拉平的层数，默认为1。<br>
如果不管有多少层嵌套，都要转成一维数组，可以用Infinity关键字作为参数。<br><br>
flatMap()方法对原数组的每个成员执行一个函数（相当于执行Array.prototype.map()），然后对返回值组成的数组执行flat()方法。该方法返回一个新数组，不改变原数组。
```javascript
// 相当于 [[2, 4], [3, 6], [4, 8]].flat()
[2, 3, 4].flatMap((x) => [x, x * 2])
// [2, 4, 3, 6, 4, 8]
```
flatMap()方法的参数是一个遍历函数，该函数可以接受三个参数，分别是当前数组成员、当前数组成员的位置（从零开始）、原数组。<br>
第二个参数，用来绑定遍历函数里面的this。
### 10、数组实例 map()
返回一个新数组，新数组中的元素为原始数组元素调用函数处理后的值。<br>
map() 不会对空数组进行检测，不会改变原始数组。
```javascript
array.map(function(currentValue,index,arr), thisValue)
```
```javascript
var numbers = [1, 5, 10, 15];
var doubles = numbers.map(function(x) {
   return x * 2;
});
// doubles is now [2, 10, 20, 30]
// numbers is still [1, 5, 10, 15] 
```
### 11、数组实例 filter()
创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。<br>
```javascript
array.filter(function(currentValue,index,arr), thisValue)
```
```javascript
var words = ["aaaaa", "ccccc", "ccccs", "sssss", "ccccs", "bbbbbbbb"];

var longWords = words.filter(function(word){
  return word.length > 6;
});

// ["bbbbbbb"]
 
```
### 12、数组实例 reduce()
接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。<br>
```javascript
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
//initialValue 传递给函数的初始值
```
```javascript 
var numbers = [0, 1, 2, 3];
 
var result = numbers.reduce(function(accumulator, currentValue) {
    return accumulator + currentValue;
});
 
console.log(result);
//6 
```
### 13、数组实例 some()
检测数组中至少一个元素是否通过所提供回调函数的条件。（注意和every()的区别）
```javascript
array.some(function(currentValue,index,arr),thisValue)
```
```javascript
function isBiggerThan10(element, index, array) {
  return element > 10;
}

[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true 
```
### 14、数组实例 every()
用于检测数组所有元素是否都符合指定条件。（注意和some()的区别）
```javascript
array.every(function(currentValue,index,arr), thisValue)
```
```javascript
function isBigEnough(element, index, array) { 
  return element >= 10; 
} 

[12, 5, 8, 130, 44].every(isBigEnough);   // false 
[12, 54, 18, 130, 44].every(isBigEnough); // true 
```

*文章内容参考阮一峰&弹指壹挥间的文章内容，如有侵权联系删除*






