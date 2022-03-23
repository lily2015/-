# React的理解
- 是什么？一句话直达本质
- 能干什么？ 用途和应用场景
- 如何干什么？核心的工作原理
- 干的怎么样？优缺点

## 是什么
- 用于构建用户界面的JS库

## 能干什么
- 可以通过组件化的方式快速构建大型web应该程序

## 如何干的
- 声明式
```js
// 我们只需要告诉程序我们要什么效果，其他的交给程序来做

let root = document.getElementById('root');

// 声明式
ReactDOM.render(<h1 onClick={() => console.log('hello')}>hello</h1>)

// 命令式
let h1 = document.createElement('h1');
h1.innerHTML = 'hello';
h1.addEventListener('click', () => console.log('hello'));
root.appendChild(h1);
```

- 组件化：方便视图拆分和复用，做到高内聚、低耦合
- 一次学习，随处编写
1. 可以开发web, android, ios, vr和命令程序
2. RN 创建原生应用，react 360 创建VR应用

## 干的怎么样
- 优点
1. 开发团队和社区强大
2. 一次学习，随处编写
3. API比较简洁

- 缺点
1. 技术选型没有官方的系统解决方案，灵活度比较高（也有一些全家桶的解决方案dva umi）
2. 组件化过于灵活，新手不容易写出高质量的代码（比如 state没用的操作）

- 其他扩展
1. JSX 实现了声明式
2. 虚拟DOM可以实现跨平台
3. React使用的设计模式（链表、小顶堆-V17增加了更新优先级的lane模型）
4. 自己React大型架构经验

# 为什么引入JSX
## 什么是JSX
- JSX是js的语法扩展，可以很好的描述UI的样子，是React.createElement的语法糖
```js
// <h1 id="title">hello<span>world</span></h1>
React.createElement('h1', 
  {
    id: 'title'
  }, 
  'hello',
  React.createElement('span', 'world')
)
```

## JSX作用
- 代码结构清晰，可读性强
- 实现代码的低耦合，方便复用和组合
- 不引入新的概念和语法，只写js

## JSX工作原理: 抽象语法树
- babel.js
1. runtime: classic 是老的转换，把jsx转换成React.createElement
2. automatic 是新的转换 import jsx，转换成jsx()
- astexplorer 

# Virtual DOM 的理解
## 实现虚拟DOM
- 像React.createElement函数所返回的就是一个虚拟DOM
- 虚拟DOM是一个描述真实DOM的纯JS对象
## 优点
- 避免了浏览器真实的dom操作，以及事件操作等的兼容问题
- 内容经过了XSS处理（渲染前会进行转义），呆以防范XSS攻击  dangerouslySetInnerHTML
- 跨平台（安卓，ios，vr）
- Diff算法，减少DOM操作
## 缺点
- 虚拟DOM操作消耗额外内存
- 首次渲染其实不一定会更快

# 函数组件和类组件的区别
```js
  // 纯函数式组件
  // 无this（state, ref, context）; 无生命周期;
  import React from 'react';
  let virtualDOM = (
    <div id="a1" key="a1">
      <div id="b2" key="b1">b1</div>
    </div>
  )
  function FunctionComponent(props) {
    return virtualDOM;
  }

  // class是个语法糖，最后也是编译成function
  class ClassComponent extends React.component {
    render() {
      return virtualDOM
    }
  }
  let functionVirtualDOM = <FunctionComponent />
  let classVirtualDOM = <ClassComponent />
  console.log(functionVirtualDOM, classVirtualDOM);
```
## 相同点
- 都可以接收属性并返回React元素
## 不同点
- 编程思想不同，类组件需要先创建实例，然后实例调用render()方法，是基于面向对象的方式编程。函数组件不需要创建实例，接收输入，返回输出。
- 内存占用：类组件创建并保存实例，会占用一定内存。函数组件不需要创建实例，可以节约内存
- 捕获特性：函数组件具有值捕获的特性（class中的this.state.number是最新的。而函数式的number是指渲染函数时的number值）
- 状态：类组件this.setState更新组件。函数组件可以使用useState修改状态。
- 生命周期：类组件有完整的生命周期，可以在生命周期内编写逻辑。函数组件可以通过useEffect实现类似生命周期的功能
- 逻辑复用：类组件可以通过继承实现逻辑复用，但官方推荐HOC优于继承，函数组件可以通过自定义hooks实现逻辑的复用
- 路过更新：类组件通过shouldComponentUpdate和PureComponent来跳过更新，而函数组件可以通过React.memo(函数)来跳过更新
  React.PureComponent继承了Component，通过props和state的浅对比来实现 shouldComponentUpate()，如果定义了 shouldComponentUpdate()，无论组件是否是 PureComponent，它都会执行shouldComponentUpdate结果来判断是否 update。
- 函数式组件更方便写单元测试

# React渲染流程
- 宏观的设计理念
- 关键原理清晰描述，抽象和具象相结合
- 结合工程实践和工作成果

## 设计理念
- 跨平台渲染 => 虚拟DOM
- 快速响应 => 异步可中断 + 增量更新
### 异步可中断 Fiber
  - Fiber 实际上是借助 浏览器提供的 window.requestIdleCallback 实现。把任务碎片化。
    只有试验版本里有
    ReactDOM.unstable_createRoot(document.getElementById('root')).render(<App />)
    ReactDOM.unstable_batchedupdates(() => {useState({})})。
  - requestIdleCallback: 就是利用浏览器的空余时间执行这些需要大量计算的任务，当空余时间结束，会中断计算任务，执行高优先级的任务，以达到不阻塞主线程任务（例如浏览器 UI 渲染）的目的。
    
    合作式调度

    目前只有chrome支持，MessageChannel + requestAnimationFrame模拟一requestIdleCallback

    运用Fiber，会延长渲染时间
    如果是动画，还是用requestAnimation

    新版本componentWillMount componentWillUpdate componentWillReceiveProps 为了异步把这三个生命周期被废弃了

### 增量更新 Diff

## 性能瓶颈
- JS任务执行时间过长: 刷新率 FPS
  表示的是每秒钟画面更新次数，当今大多数设备的屏幕刷新率都是60次/秒，在两次硬件刷新之间浏览器进行两次重绘是没有意义的只会消耗性能，那么浏览器渲染动画或页面的每一帧的速率，也需要跟设备的刷新率保持一致。
  也就是说，浏览器对每一帧画面的渲染工作需要在16.6ms（1000ms/60）之内完成，也就是说每一次渲染都要在 16ms才不会掉帧。
  在这16ms 内浏览器要完成的工作有：
  脚本执行（JavaScript）：脚本造成了需要重绘的改动，比如增删 DOM、请求动画等
  样式计算（CSS Object Model）：级联地生成每个节点的生效样式。
  布局（Layout）：计算布局，执行渲染算法
  重绘（Paint）：各层分别进行绘制（比如 3D 动画）
  合成（Composite）：将位图发送给合成线程。
  如果某次渲染花了20ms时间，那么他的渲染效果不会再浏览器第一帧16ms的时候显示，这个渲染结果会在第一帧32ms的时候显示。这就掉了一帧。

## React 16+ 的渲染流程
- scheduler 调度，选择高优先级的任务进入reconciler(调节器)
- reconciler 计算变更的内容 DIFF算法
- Renderer commit react-dom 把变更的内容渲染到页面上

## 构建Fiber
- 根据虚拟DOM nextChildren DOM是老的Fiber和新的Fiber的比较






