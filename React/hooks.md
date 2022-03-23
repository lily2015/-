## useState()
语法：
  [xxx, setXxx] = React.useState(initValue)

setXxx()的两种写法：
  setXxx(newValue): 参数为非函数值，直接指定新的状态值，内部用其覆盖原来的状态值
  setXxx(value => newValue): 参数为函数，接收原本的状态值，返回新的状态值

## useEffect() 副作用
语法：
  useEffect(() => {
    // 在些执行任何带副作用的操作
    return () => {
      // 在组件卸载前执行，在些做些收尾工作，比如清除定时器/取消订阅等
    }
  }, [])

各项说明：
  第一个函数：useEffect调用执行时的函数
  第二个[]，有监测的作用：
    1、如果不加，相当于监测所有更新，useEffect()执行 1+n 次，此时模拟 componentDidMount() + componentDidUpdate()
    2、如果是空[]，相当于谁也不监测，useEffect()执行 1 次，此时模拟 componentDidMount()
    3、如果是[count], 相当于监测count的变化，useEffect()执行 1 + 值变化的次数
  return的函数：在组件卸载前执行，模拟 componentWillUnmount()

可在副作用中操作：
  发ajax请求获取数据
  设置订阅 / 启动定时器
  手动更改真实DOM

### useRef() 功能同React.createRef()
语法：
  const refContainer = React.useRef()
  <input type="text" ref={refContainer} />
