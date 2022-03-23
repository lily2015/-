# 预编译
- 作用域(全局作用域和函数作用域)的创建阶段 预编译的阶段
- 预编译的时候做了哪些事情
- 作用域分为全局作用域和函数作用域
- 函数作用域的创建阶段有一个与之对应的 js的变量对象 也称为AO对象，供js引擎自己去访问的
- 1、创建AO对象 2、找形参和变量的声明 作为AO对象的属性名 值是undefined 3、实参和形参相统一 4、找函数声明 会覆盖变量声明
- js的解释执行 逐行执行

```js
  function fn(a, c) {
    console.log(a) // function a() {}
    var a = 123
    console.log(a) // 123
    console.log(c) // function c() {}
    function a() {}
    if (false) {
      var d = 789
    }
    console.log(d) // undefined
    console.log(b) // undefined
    var b = function() {}
    console.log(b) // function() {}
    function c() {}
    console.log(c) // function c() {}
  }
  fn(1, 2)

/**
  AO {
    a: undefined 1 function a() {}
    c: undefined 2 function c() {}
    d: undefined
    b: undefined
  }
 */
```

# this
- 在函数中直接使用，指向window
- 函数作为对象的方法被调用(谁调用我 我就指向谁)
```js
  var name = 222
  var a = {
    name: 111,
    say: function() {
      console.log(this.name)
    }
  }

  var fun = a.say
  fun()  // fun.call(window) // 222
  a.say() // a.say.call(a) // 111

  var b = {
    name: 333,
    say: function (fun) {
      fun() // fun.call(window) // 222
    }
  }
  b.say(a.say)
  b.say = a.say // 相当于b.say = function() {console.log(this.name)}
  b.say() // b.say.call(b) // 333
```
