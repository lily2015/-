### 理解
- Error boundary 用来捕获后代组件错误，渲染备用页面

### 特点
- 只能捕获后代组件生命周期产生的错误，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误

### 使用方式
- getDerivedStateFromError 配合componentDidCatch
  
```js
// 生命周期函数，一旦后代组件报错就会触发
static getDerivedStateFromError (error) {
  console.log(error)
  return {
    hasError: true
  }
}

componentDidCatch (error, info) {
  // 统计页面错误，发送请求到后台
  console.log(error, info)
}
```
