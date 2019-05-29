## String
### 1、字符串是对象吗？
```javascript
let a = "sss";
let b = new String("sss");
console.log(a==b);//true
console.log(a===b);//false
console.log(typeof a); //string
console.log(typeof b);//object
```
字符串的申明方式不一样，也会导致其成为不同的类型。
我的理解：在Java中string是引用类型，JS是弱类型语言，将字符串归于基本类型，却存在String这样的构造函数，这感觉很矛盾，但是不影响开发中的使用，因为，引用类型的字符串所存在的属性和方法，基本类型的也同样适用。
### 2、字符串的属性和方法
```javascript
console.log(new String);
```
结果如图：
![string](https://raw.githubusercontent.com/yangzaiwangzi/learningNotes/master/img/string.jpg)
可以清楚的看到string的属性和方法。
#### 2.1、属性
constructor
length
prototype
#### 2.2、方法
常用的如下，不会都介绍。
##### 2.2.1 charAt()、charCodeAt()
```javascript
const str = "asdfgh";
//接受一个参数，默认传0，返回在指定位置的字符；
console.log(str.charAt(2));//d
//接受一个参数，默认传0，返回在指定的位置的字符的 Unicode 编码
console.log(str.charCodeAt(2));//100
```
##### 2.2.2 concat()
连接两个或更多字符串，并返回新的字符串，通常用‘+’代替。
##### 2.2.3 fromCharCode()
将 Unicode 编码转为字符
```javascript
String.fromCharCode(100);//d
```
这不是实例对象上的方法，在上面图片中的 ‘constructor’ 属性中可以看到它，所以，它是构造函数的一个方法。
##### 2.2.4 indexOf()、lastIndexOf()
```javascript
const str = "asdfgh";
//从左向右检索，返回字符串中首次出现的下标，没有则-1；
console.log(str.indexOf('d'));//2
//从右向左检索，返回字符串中首次出现的下标，没有则-1；
console.log(str.lastIndexOf('d'));//6
```
##### 2.2.5 search()、match()
```javascript
const str = "abluesddddfblueghd"; 
// search()
//从左向右检索，返回字符串中首次出现符合匹配规则（可以传入正则规则）的下标，没有则-1；
//类似indexOf()，区别是一个可以匹配正则
console.log(str.search('d'));// 6
console.log(str.search('D'));// -1
console.log(str.search(/blue/i));// 1 
//match()
//从左向右检索，返回字符串中符合匹配规则（可以传入正则规则）的数组，没有则null；
//可以返回一个或是多个，都是数组
var str = 'gagdfgadfgdg';
var _str1 = str.match(/.gd/);//匹配一个
var _str2 = str.match(/.gd/g);//全局匹配多个
console.log(_str1);//["agd", index: 1, input: "gagdfgadfgdg", groups: undefined]
console.log(_str2);// ["agd", "fgd"]
```
##### 2.2.6 replace()
在字符串中查找匹配的子串， 并替换与正则表达式匹配的子串
```javascript
//可用空来替换，相当于删除
const str = 'abc33abcabcabcab33cabc';
const _str1 = str.replace(/33/g,''); 
console.log(_str1); //abcabcabcabcabcabc
//全局替换
const str = 'abc33abcabcabcab33cabc';
const _str1 = str.replace(/33/g,'444'); 
console.log(_str1); //abc444abcabcabcab444cabc
//局部替换
const str = 'abc33abcabcabcab33cabc';
const _str1 = str.replace(/33/,'444'); 
console.log(_str1); //abc444abcabcabcab33cabc
//用下标替换
const str = 'abc33abcabcabcab33cabc';
const _str1 = str.replace(3,'444'); 
console.log(_str1); //abc4443abcabcabcab33cabc
```
##### 2.2.7 split(value,n)
把字符串分割为字符串数组
vlaue：分割的元素，可为空字符串
n：数值，控制最终返回值数组的长度最大值。
```javascript
const str = 'abc33ab33cabc';
const _str0 = str.split(""); 
const _str1 = str.split("33"); 
const _str2 = str.split("33",2); 
console.log(_str0); // ["a", "b", "c", "3", "3", "a", "b", "3", "3", "c", "a", "b", "c"]
console.log(_str1); // ["abc", "ab", "cabc"]
console.log(_str2); // ["abc", "ab"]
```
##### 2.2.8 slice()、substr()、substring()
- slice(startIndex.endIndex)
传入开始和结束的下标，截取中间需要的字符串
startIndex必传 可以为负数，即倒数，最后一位即为-1；
endIndex选传 不传则默认到最后一位 **截取时不包括该位置**，可以为负数，即倒数，最后一位即为-1；
```javascript
const str = 'abcd';
const _str1 = str.slice(1);
const _str2 = str.slice(1,2); 
const _str3 = str.slice(1,-1);  
console.log(_str1);//bcd
console.log(_str2);//c
console.log(_str3);//bc
```
- substr(startIndex，length)
传入开始和所需的长度，截取中间需要的字符串
startIndex必传 可以为负数，即倒数，最后一位即为-1；
length选传 截取的长度
```javascript
const str = 'abcd';
const _str1 = str.substr(1);
const _str2 = str.substr(1,2);  
console.log(_str1);//bcd
console.log(_str2);//bc
```
- substring(startIndex,endIndex)
传入开始和结束的下标，截取中间需要的字符串，和slice相似
startIndex必传 不可为负数，若为负数，则为0
endIndex选传 不可为负数，若为负数，则为0
```javascript
const str = 'abcd';
const _str1 = str.substring(1,2);
const _str2 = str.slice(-1,-2); 
const _str3 = str.slice(0,0);  
console.log(_str1);//b
console.log(_str2);// =>空字符串
console.log(_str3);// =>空字符串
```
- 三者区别
1、第2个参数。slice，substring中表示字符串的结束位置，substr中表示长度。
2、参数可否为负数。slice两个参数都可以为负数，substr只有第一个参数可以为负数，substring两个参数都为非负数
3、第1个参数大于第2个参数时：slice则返回空字符串；substring交换参数位置，继续截取；substr不受影响；
##### 2.2.9 trim()
去除首位空字符串
##### 2.2.10 toLowerCase()、toUpperCase()
大小写切换
#### 3、ES6对字符串的扩展
##### 3.1 includs()、startsWith(str,index)、endsWith(str,index)
- includs(str,index)
返回布尔值，原字符串是否含有str，有则true，无false；可代替indexOf()来判断是否含有某字符串
str：需要匹配的字符串
index：开始匹配的位置（相当于截取 index~尾部 的字符串在来匹配）
- startsWith(str,index)
返回布尔值，原字符串是否是str开头，有则true，无false；
str：需要匹配的字符串
index：开始匹配的位置（相当于截取 index~尾部 的字符串在来匹配）
- endsWith(str,index)
返回布尔值，原字符串是否是str结尾，有则true，无false；
str：需要匹配的字符串
index：开始匹配的位置（相当于截取 0~index 的字符串在来匹配）
##### 3.2 repeat()
- str.repeat(n)
将str循环n遍，得到新字符串；
n  >-1&&n != Infinity；否则报错；其中大于0的小数统统向下取整；
```javasript
console.log('a'.repeat(5));//aa
console.log('a'.repeat(5.6));//aa
console.log('a'.repeat(-0.5)); // =>向上取整为0
```
##### 3.3 string.padStart(length, str)、string.padEnd(length, str)
将string用str不全到length的长度；
若str过长，可删除适当str，再补进string；
string长度超多length，则string不变
一个从头补padStart()，一个从尾补padEnd()；
弄清楚谁补谁！！！参数补到调用者里
```javasript
console.log('xyz'.padStart(6,'abc'));//abcxyz
console.log('xyz'.padEnd(5,'abc'));//xyzab
console.log('xyzxyz'.padStart(5,'abc'));//xyzxyz
//适用场景
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```
##### 3.4 字符串的遍历器接口
因new String 含有[Symbol.iterator],则其默认被设置遍历器接口，可通过for...of..进行遍历；
#### 参考
**[ECMAScript 6 入门-字符串的扩展](http://es6.ruanyifeng.com/#docs/string)**
