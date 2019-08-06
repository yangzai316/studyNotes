### 路由
- hash

hash只是客户端的一种状态，不会被发送到服务端<br>
window.onhashchange监听hash变化<br>

- history

window.history.pushState()<br>
window.history.replaceState()<br>
window.history.popstate()<br>
在浏览历史中添加历史记录,但是并不触发跳转；<br>
每当同一个文档的浏览历史（即history对象）出现变化时，就会触发popstate事件<br>

---

### call、apply、bind
- 含义
借用方法<br>
改变函数执行时的this指向

``` javascript
fun.call(thisArg, param1, param2, ...)
fun.apply(thisArg, [param1,param2,...])
fun.bind(thisArg, param1, param2, ...)
```

fun的this指向thisArg对象

- 区别

| 方法名 | 参数 | 立即执行 | 返回 |
| ----- | ---- | ---- | ---- |
| call | n个参数 | 是 |返回执行的结果|
| apply | 2个参数,第二参数为数组 | 是 |返回执行的结果|
| bind | n个参数 | 否 |返回改变了上下文后的函数，保留原始参数|

- 使用实列

call：数据类型判断【Object.prototype.toString.call(data)】<br>
apply:求数组最大值【Math.max.apply(Math,[data])】<br>
bind:回调函数中This的丢失<br>

- 原生实现call、apply、bind

*[参考文章](https://juejin.im/post/5d469e0851882544b85c32ef)*

---

### display:none;、visibility: hidden;、opacity: 0;
- 结构：

display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击<br>
visibility: hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击<br>
opacity: 0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击<br>

- 继承：

display: none和opacity: 0：是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示<br>
visibility: hidden：是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式<br>

- 性能：

displaynone : 修改元素会造成文档回流,读屏器不会读取display: none元素内容，性能消耗较大<br>
visibility:hidden: 修改元素只会造成本元素的重绘,性能消耗较少读屏器读取visibility: hidden元素内容<br>
opacity: 0 ： 修改元素会造成重绘，性能消耗较少<br>
