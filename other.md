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
