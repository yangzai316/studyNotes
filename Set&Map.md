# Set 和 Map 数据结构
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。
#### 1、set
Set 本身是一个构造函数，用来生成 Set 数据结构。
```javascript
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
//通过add方法向 Set 结构加入成员，结果表明 Set 结构不会添加重复的值
```
Set 函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。
```javascript
// 例一
const set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]

// 例二
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

// 例三
const set = new Set(document.querySelectorAll('div'));
set.size // 56

// 类似于
const set = new Set();
document.querySelectorAll('div').forEach(div => set.add(div));
set.size // 56

// 上面代码也展示了一种去除数组重复成员的方法:
[...new Set(array)]
```
向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。<br>
Set 内部判断两个值是否不同，类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身。<br>
在 Set 内部，两个NaN是相等,两个对象总是不相等的。
#### 2、Set 实例的属性和方法
- 属性：<br>
Set.prototype.constructor：构造函数，默认就是Set函数。<br>
Set.prototype.size：       返回Set实例的成员总数。
- 方法：<br>
add(value)：               添加某个值，返回 Set 结构本身。<br>
delete(value)：            删除某个值，返回一个布尔值，表示删除是否成功。<br>
has(value)：               返回一个布尔值，表示该值是否为Set的成员。<br>
clear()：                  清除所有成员，没有返回值。
- 遍历方法<br>
keys()：   返回键名的遍历器<br>
values()： 返回键值的遍历器<br>
entries()：返回键值对的遍历器<br>
forEach()：使用回调函数遍历每个成员<br>

#### 3、Array.from方法可以将 Set 结构转为数组。
#### 4、WeakSet
WeakSet 结构与 Set 类似，也是不重复的值的集合。<br>
但是，它与 Set 有两个区别：<br>
- WeakSet 的成员只能是对象，而不能是其他类型的值，不是对象，加入 WeaKSet 就会报错
- WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用
- WeakSet 不可遍历<br>
WeakSet 是一个构造函数，可以使用new命令，创建 WeakSet 数据结构<br>
作为构造函数，WeakSet 可以接受一个数组或类似数组的对象作为参数<br>
- 方法：<br>
WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。<br>
WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。<br>
WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。<br>
WeakSet 没有size属性，没有办法遍历它的成员（是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。）








