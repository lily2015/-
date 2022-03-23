# 从 var 的局限性（不合理性）的角度来理解const let

## var 声明提升 —— 先上车，后买票
```js
console.log(a) // undefined
var a = '1'
```

```js
console.log(a) // 发生报错
const a = '1'
```

## var 变量覆盖 —— 套牌车
```js
var a = 1
var a = 2
console.log(a) // 2
```

```js
let a = 1
let a = 2
// 发生报错
```

## var 没有块级作用域 —— 红杏出墙
```js
for (var i = 0; i < 5; i++) {
  // 
}
console.log(i) // 5
```

```js
for (let i = 0; i < 5; i++) {
  // 
}
console.log(i) // 报错：i is not defined
```
