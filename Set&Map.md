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
- 遍历方法(Map 的遍历顺序就是插入顺序。):<br>
keys()：   返回键名的遍历器<br>
values()： 返回键值的遍历器<br>
entries()：返回键值对的遍历器<br>
forEach()：使用回调函数遍历每个成员<br>

#### 3、Array.from方法可以将 Set 结构转为数组。
#### 4、WeakSet
WeakSet 结构与 Set 类似，也是不重复的值的集合。<br>
但是，它与 Set 有区别：<br>
- WeakSet 的成员只能是对象，而不能是其他类型的值，不是对象，加入 WeaKSet 就会报错
- WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用
- WeakSet 不可遍历<br>
<br>
WeakSet 是一个构造函数，可以使用new命令，创建 WeakSet 数据结构<br>
作为构造函数，WeakSet 可以接受一个数组或类似数组的对象作为参数<br>
- 方法：<br>
WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。<br>
WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。<br>
WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。<br>
WeakSet 没有size属性，没有办法遍历它的成员（是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。）
#### 5、Map
构造函数<br>
它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。<br>
Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。<br>
Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组：
```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.get('name') // "张三"
map.get('title') // "Author"
```
不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构都可以当作Map构造函数的参数。<br>
如果对同一个键多次赋值，后面的值将覆盖前面的值。<br>
如果读取一个未知的键，则返回undefined。<br>
Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。
属性和操作方法：<br>
- size          返回 Map 结构的成员总数<br>
set(key, value) 设置键名key对应的键值为value<br>
get(key)      读取key对应的键值<br>
has(key)      返回一个布尔值，表示某个键是否在当前 Map 对象之中<br>
delete(key)   方法删除某个键，返回true。如果删除失败，返回false<br>
clear()       清除所有成员，没有返回值<br>

- 遍历方法(遍历顺序就是插入顺序。)：<br>
keys()：返回键名的遍历器。<br>
values()：返回键值的遍历器。<br>
entries()：返回所有成员的遍历器。<br>
forEach()：遍历 Map 的所有成员。<br>
#### 6、Map与其他数据结构的互相转换
（1）Map 转为数组：使用扩展运算符（...）
```javascript
const myMap = new Map()
  .set(true, 7)
  .set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```
（2）数组 转为 Map：将数组传入 Map 构造函数
```javascript
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
// Map {
//   true => 7,
//   Object {foo: 3} => ['abc']
// }
```
（3）Map 转为对象：如果所有 Map 的键都是字符串，它可以无损地转为对象<br>
（4）对象转为 Map<br>
（5）Map 转为 JSON<br>
（6）JSON 转为 Map<br>
#### 7、WeakMap
WeakMap结构与Map结构类似，也是用于生成键值对的集合。<br>
WeakMap与Map的区别有两点：<br>
- WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名，否则报错。
- WeakMap的键名所指向的对象，不计入垃圾回收机制（弱引用）。
- 没有遍历操作。
<br><br>
方法可用：<br>
- get()
- set()
- has()
- delete()。


























