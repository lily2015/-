## PureComponent
- 是react实现的功能等同于shouldComponentUpdate的形式，会对state/props做浅比较，如果传入的state/props的指针发生变化，则触发render方法，如果指针不变，但修改了其中的元素（数组）或者属性（对象）， PureComponent组件则不会调用render方法。
- 在使用react时，修改数组元素时，不推荐用push/unshift等数组操作方法的原因，也是考虑以后使用PureComponent的情况。推荐用扩展符的形式更新数据
```js
// 不推荐
const arr1 = ['vue', 'angular']
arr.unshift('react')  // arr : ['react', 'vue', 'angular']
this.state(arr1) // 在使用PureComponent时，不触发render

// 推荐
const arr2 = ['vue', 'angular']
this.state([
  'react',
  ...arr2
])
```

### this.props.children

### this.props.render()

