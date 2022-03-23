## context 组件间有通信方式，常用于[祖组件]与[后代组件]间通信，用于组件封装
语法:
  1、创建Context的容器对象，这个容器需要放到ABC都能访问到位置
    const XxxContext = React.createContext()
  2、渲染子组件时，外面包裹XxxContext.Provider，通过value属性给后代传值
    <XxxContext.Provider value={数据}>
      子组件
    </XxxContext.Provider>
  3、后代组件读数据：两种方式
    （1）仅适用于类组件
        static contextType = xxxContext // 声明接收
        this.context // 读取context中的value数据
    （2）函数组件、类组件都可以用
        <XxxContext.Consumer>
          {
            value => { // value就是context中的value数据
              要显示的内容
            }
          }
        </XxxContext.Consumer>

```js
class A extends React.component {
  state = {
    username: 'Tom'
  }

  const MyContext = React.createContext()

  render() {
    return (
      <>
        <h3>我是A组件</h3>
        <h4>我的用户名是：{this.state.username}</h4>
        <MyContext.Provider>
          <B />
        </MyContext.Provider>
      </>
    )
  }
}

class B extends React.component {
  render() {
    return (
      <>
        <h3>我是B组件</h3>
        <C />
      </>
    )
  }
}

// 类组件
// class C extends React.component {
//   static contextType = MyContext

//   render() {
//     console.log(this.context)
//     return (
//       <>
//         <h3>我是C组件</h3>
//         <h4>我从A组件收到的用户名是：？？？</h4>
//       </>
//     )
//   }
// }

// 函数组件
function C () {
  return (
    <>
      <h3>我是C组件</h3>
      <h4>我从A组件收到的用户名是：
        <MyContext.Consumer>
          {
            value => value.username
          }
        </MyContext.Consumer>
      </h4>
    </>
  )
}
```