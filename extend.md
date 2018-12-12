# 浅拷贝&深拷贝
### 1、什么是拷贝？
百度百科的解释：
> 拷贝（kǎobèi）是由英文copy的音译词，copy意为复制、摹本。<br>

本文的解释（白话）：
有一个已知的元素，我们叫源头（origin），我们想得到一个新的（new）和源头一摸一样但完全独立的元素。
### 2、基本类型的拷贝
```javascript
let a = 100;
let b = a;
console.log(a);     //100
console.log(b);     //100
//完成拷贝，修改一下，测试是否独立
b = 111;
console.log(a);     //100
console.log(b);     //111
//测试完成，完成拷贝，完全独立
```
结论：基本对象的拷贝就是简单的复制，这是栈内存存储的原因，没有浅拷贝和深拷贝的概念，不是本文的重点讨论内容，一带而过，下面的内容也不会再考虑基本类型，
则合理声明一下，这也就是很多文章，直接讨论对象拷贝的原因。
### 3、引用类型的拷贝
#### 3.1、什么是浅拷贝
就是原对象中的**没有嵌套关系，只是简单的基本类型组成属性**被拷贝到新对象中，且得到了完全独立，而方法、函数、嵌套的对象，都只是拷贝的相应的引用地址，
无法实现完全独立。
#### 3.2、什么是深拷贝
是浅拷贝的加大版本，实现了新对象在各个属性、方法...，完全和源对象的分离，完全独立存在，二者不在相互干扰。
#### 3.3、数组的拷贝
```javascript
let arr1 = [1, 2];
let arr2 = arr1.slice();
console.log(arr1); //[1, 2]
console.log(arr2); //[1, 2]
//完成拷贝，修改一下，测试是否独立
arr2[0] = 3; //修改arr2
console.log(arr1); //[1, 2]
console.log(arr2); //[3, 2]
//测试完成，完成拷贝，完全独立
```
是不是数组就可以这样，显然不是，看下面：

```javascript
let arr1 = [1, 2, [3, 4]];
let arr2 = arr1.slice();
console.log(arr1); //[1, 2, [3, 4]]
console.log(arr2); //[1, 2, [3, 4]]
//完成拷贝，修改一下，测试是否独立
arr2[2][1] = 5; 
console.log(arr1); //[1, 2, [3, 5]]
console.log(arr2); //[1, 2, [3, 5]]
//测试失败，拷贝不完全，无法实现独立
```
结论：该方法无法实现需求的拷贝，其实这里实现的就是一个浅拷贝，如果项目中无需涉及深拷贝，可用该方法，数组的基本方法中，凡可以返回新数组的，
都可以实现该功能，如：concat()...
#### 3.4、对象的拷贝
- Object.assign()
```javascript
let obj1 = {x: 1, y: 2};
let obj2 = Object.assign({}, obj1);
console.log(obj1) //{x: 1, y: 2}
console.log(obj2) //{x: 1, y: 2}
//完成拷贝，修改一下，测试是否独立
obj2.x = 2;
console.log(obj1) //{x: 1, y: 2}
console.log(obj2) //{x: 2, y: 2}
//测试完成，完成拷贝，完全独立
//试试嵌套
var obj1 = {
    x: 1, 
    y: {
        m: 1
    }
};
var obj2 = Object.assign({}, obj1);
console.log(obj1) //{x: 1, y: {m: 1}}
console.log(obj2) //{x: 1, y: {m: 1}}
//完成拷贝，修改一下，测试是否独立
obj2.y.m = 2;
console.log(obj1) //{x: 1, y: {m: 2}}
console.log(obj2) //{x: 2, y: {m: 2}}
//测试失败，拷贝不完全，无法实现独立
```
结论：Object.assign()是ES6的内容，为合并对象而用，这里可以实现浅拷贝。
- JSON.parse(JSON.stringify(obj))
```javascript
var obj1 = {
    x: 1, 
    y: {
        m: 1
    }
};
var obj2 = JSON.parse(JSON.stringify(obj1));
console.log(obj1) //{x: 1, y: {m: 1}}
console.log(obj2) //{x: 1, y: {m: 1}}
//完成拷贝，修改一下，测试是否独立
obj2.y.m = 2; 
console.log(obj1) //{x: 1, y: {m: 1}}
console.log(obj2) //{x: 2, y: {m: 2}}
//测试完成，完成拷贝，完全独立
```
结论：*基本*实现深拷贝
MDN文档曾经说过
> undefined、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）。
```javascript
var obj1 = {
    x: 1,
    y: undefined,
    z: function add(z1, z2) {
        return z1 + z2
    },
    a: Symbol("foo")
};
var obj2 = JSON.parse(JSON.stringify(obj1));
console.log(obj1) //{x: 1, y: undefined, z: ƒ, a: Symbol(foo)}
```
结论：JSON.parse(JSON.stringify(obj))基本实现需求，但不适用undefined、任意的函数以及 symbol 值。
- 自行封装<br>
机理：循环使用浅拷贝，遇到object的元素，则对该元素循环使用浅拷贝，反反复复，知道结束，这里就用到循环+递归。
```javascript
function deepCopy(obj) {
    let result = {}//即将return的新对象
    let keys = Object.keys(obj),
        key = null,
        temp = null;
    for (let i = 0; i < keys.length; i++) {
        key = keys[i];    
        temp = obj[key]; 
        if (temp && typeof temp === 'object') {// 遇到自己，调用自己（递归） 
            result[key] = deepCopy(temp);
        } else { // 否则直接赋值给新对象
            result[key] = temp;
        }
    }
    return result;
}
var obj1 = {
    x: {
        m: 1
    },
    y: undefined,
    z: function add(z1, z2) {
        return z1 + z2
    },
    a: Symbol("foo")
};
var obj2 = deepCopy(obj1);
obj2.x.m = 2;
console.log(obj1); //{x: {m: 1}, y: undefined, z: ƒ, a: Symbol(foo)}
console.log(obj2); //{x: {m: 2}, y: undefined, z: ƒ, a: Symbol(foo)}
```
结论：实现深拷贝，数组、undefined、任意的函数以及 symbol都始用。
- 优化<br>
以上方法在遇到其中一个属性是自己的时候，会进入反复递归，导致爆栈（内存爆了），如下：
```javascript
var obj1 = {
    x: 1, 
    y: 2
};
obj1.z = obj1;
var obj2 = deepCopy(obj1);
//这种情况就会出现爆栈，不用担心字面量声明引用自己，那样引用结果为undefined
```
优化产物：
```
function deepCopy(obj, parent = null) {
    let result = {};
    let keys = Object.keys(obj),
        key = null,
        temp= null,
        _parent = parent;
    while (_parent) {// 该字段有父级则需要追溯该字段的父级
        // 如果该字段引用了它的父级则为循环引用
        if (_parent.originalParent === obj) { 
            return _parent.currentParent; // 循环引用直接返回同级的新对象
        }
        _parent = _parent.parent;
    }
    for (let i = 0; i < keys.length; i++) {
        key = keys[i];
        temp= obj[key];
        if (temp && typeof temp=== 'object') { 
            result[key] = deepCopy(temp, {// 递归执行深拷贝 将同级的待拷贝对象与新对象传递给 parent 方便追溯循环引用
                originalParent: obj,
                currentParent: result,
                parent: parent
            });
        } else {
            result[key] = temp;
        }
    }
    return result;
}
var obj1 = {
    x: 1, 
    y: 2
};
obj1.z = obj1;
var obj2 = deepCopy(obj1);
```
结论：完美实现深拷贝。如需要拷贝原型链上的属性，可始用for...in...，进行循环处理，在里面可通过hasOwnProperty()来开关这个需求。
##### 参考文章
[一篇文章彻底说清 JS 的深拷贝/浅拷贝](https://mp.weixin.qq.com/s/FoNX_Vn1Xy0pElr3GyTgbw)<br>
[低门槛彻底理解JavaScript中的深拷贝和浅拷贝](https://mp.weixin.qq.com/s/FoNX_Vn1Xy0pElr3GyTgbw)
