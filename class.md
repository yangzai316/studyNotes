# class
### 基础知识
JavaScript 语言中，生成实例对象的传统方法是通过构造函数。<br>
ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。
``` javascript
//定义类
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```
ES6 的类，完全可以看作构造函数的另一种写法.
```javascript
class Point {
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true
```
类的数据类型就是函数，类本身就指向构造函数。
使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致。
```javascript
class Bar {
  doStuff() {
    console.log('stuff');
  }
}

var b = new Bar();
b.doStuff() // "stuff"
```
```javascript
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}
// 等同于
Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
```
在类的实例上面调用方法，其实就是调用原型上的方法。
类的内部所有定义的方法，都是不可枚举的（non-enumerable）,这一点与 ES5 的行为不一致。
### 严格模式
类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。<br>
考虑到未来所有的代码，其实都是运行在模块之中，所以 ES6 实际上把整个语言升级到了严格模式。
### constructor 
constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加。<br>
constructor方法默认返回实例对象（即this），完全可以指定返回另外一个对象。<br>
类必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。<br>
与 ES5 一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```
与 ES5 一样，类的所有实例共享一个原型对象。
```javascript
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__ === p2.__proto__
//true
```
### Class 表达式
与函数一样，类也可以使用表达式的形式定义。
```javascript
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};
//这个类的名字是MyClass而不是Me，Me只在 Class 的内部代码可用，指代当前类。Me只在 Class 内部有定义。
//如果类的内部没用到的话，可以省略Me。
const MyClass = class { 
  /* ... */ 
};
```
### 不存在变量提升
类不存在变量提升（hoist），这一点与 ES5 完全不同。
### name 属性
name属性总是返回紧跟在class关键字后面的类名。
```javascript
class Point {}
Point.name // "Point"
```
### Class 的静态方法
类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。<br>
```
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()  // TypeError: foo.classMethod is not a function

//如果静态方法包含this关键字，这个this指的是类，而不是实例。
class Foo {
  static bar () {
    this.baz();
  }
  static baz () {
    console.log('hello');
  }
  baz () {
    console.log('world');
  }
}

Foo.bar() // hello
//从这个例子还可以看出，静态方法可以与非静态方法重名。
//父类的静态方法，可以被子类继承。
```
### new.target 属性
new是从构造函数生成实例对象的命令。<br>
ES6 为new命令引入了一个new.target属性，该属性一般用在构造函数之中，返回new命令作用于的那个构造函数。<br>
如果构造函数不是通过new命令调用的，new.target会返回undefined，因此这个属性可以用来确定构造函数是怎么调用的。
