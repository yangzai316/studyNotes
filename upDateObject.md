# ES对对象的扩展
#### 属性和方法的简洁表示法
```javascript
//属性：
  const baz = {foo};
  //等同于
  const baz = {foo: foo};
//方法：
  const o = {
    method() {
      return "Hello!";
    }
  };

  // 等同于

  const o = {
    method: function() {
      return "Hello!";
    }
  };
```
简洁写法的属性名总是字符串，这会导致一些看上去比较奇怪的结果。
```javascript
const obj = {
  class () {}
};
// 等同于
var obj = {
  'class': function() {}
};
上面代码中，class是字符串，所以不会因为它属于关键字，而导致语法解析报错。
某个方法的值是一个 Generator 函数，前面需要加上星号。
const obj = {
  * m() {
    yield 'hello world';
  }
};
```
#### 属性名表达式
JavaScript 定义对象的属性，有两种方法。
```javascript
// 方法一
obj.foo = true;

// 方法二
obj['a' + 'bc'] = 123;
```
ES6 允许字面量定义对象时，可表达式作为对象的属性名，表达式还可以用于定义方法名，即把表达式放在方括号内。<br>
注意，属性名表达式与简洁表示法，不能同时使用，会报错。
```javascript
let propKey = 'foo';

let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};

let obj = {
  ['h' + 'ello']() {
    return 'hi';
  }
};

obj.hello() // hi

//注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心。
const keyA = {a: 1};
const keyB = {b: 2};

const myObject = {
  [keyA]: 'valueA',
  [keyB]: 'valueB'
};

myObject // Object {[object Object]: "valueB"}
//上面代码中，[keyA]和[keyB]得到的都是[object Object]，所以[keyB]会把[keyA]覆盖掉，而myObject最后只有一个[object Object]属性。
```
#### 方法的 name 属性 
函数的name属性，返回函数名。<br>
对象方法也是函数，因此也有name属性。<br>
有特殊情况。
```javascript
const person = {
  sayName() {
    console.log('hello!');
  },
};

person.sayName.name   // "sayName"
```
#### Object.is()
ES5 比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。<br>
它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0。<br>
JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。<br>
ES6 提出同值相等算法，用来解决这个问题。<br>
Object.is就是部署这个算法的新方法，它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。
```javascript
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false

+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```
#### Object.assign()









