
## 在函数中直接使用, 函数的独立调用就指向window
```js
  function get(content) {
    console.log(content)
  }
  get('你好') // 其实就是get.call(window, '你好')的语法糖
  get.call(window, '你好')
```

## 函数作为对象的方法被调用(谁调用我 我就指向谁)
```js
  var person = {
    name: '张三',
    run: function (time) {
      console.log(`${this.name}在跑步 最多${time}min就不行了`)
    }
  }
  person.run(30)
  person.run.call(person, 30)
```

## 箭头函数中的this
- 箭头函数中的this是在定义函数的时候绑定，而不是在执行函数的时候绑定
- 箭头函数中，this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本【没有自己的this】，导致内部的this就是【外层代码块的this】。正是因为它没有this，所以也就【不能用作构造函数】。

- 箭头函数中的this是在定义函数的时候绑定
```js
  var x = 11;
  var obj = {
    x: 22,
    say: () => {
      console.log(this.x);
    }
  }
  obj.say(); // 11 // this 指向window
```

```js
  var obj = {
    birth: 1990,
    getAge: function() {
      var b = this.birth; // 1990
      var fn = () => new Date().getFullYear() - this.birth; 
      // 箭头函数是在getAge函数里面定义的，因此，getAge方法的父执行上下文是obj
      return fn();
    }
  }
  obj.getAge(); // 28
```