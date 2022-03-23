## 事件修饰符
1. .prevent: 阻止默认事件
2. .stop: 阻止事件冒泡
3. .once: 事件只触发一次
4. .capture: 使用事件的捕获模式
5. .self: 只有event.target是当前操作的元素时才触发事件
6. .passive: 事件的默认行为立即执行，无需等待事件回调执行完毕

## 按键修饰符
1. .enter
2. .tab
3. .delete (捕获“删除”和“退格”键)
4. .esc
5. .space
6. .up
7. .down
8. .left
9. .right

## 输入修饰符
1. .lazy
2. .number
3. .trim

## 双向数据绑定
## 数据监测的原理（Object.defineProperty）

## $nextTick的原理

## vue 监视对象与监视数组有什么区别
## 动态追加一个属性的方法($set，以及$set的局限性)
push：追加一个元素
pop：删除最后一个
shift：删除第一个
unshift：在最前加一个
splice：在指定位置，增加、删除、替换
sort：排序
reverse：反转
($set)只能对data中已定义的对象或数组进行追加，不能直接创建一个对象或数组作为根节点

## key 的作用与原理(用itm.id 与 index作为key值有什么区别)

## 过滤器
<p>{{time | timeFormatter('YYYY_MM_DD')}}</p>
<p>{{time | timeFormatter}}</p>
filters: {
  timeFormatter(value, str = 'YYYY年MM月DD日 HH:mm:ss') {
    return 'value'
  }
}
Vue.filter(name, callback)

## mixin
mixins: []
Vue.mixin()

## plugins
{
  install (Vue, options) { }
}
Vue.use(plugins)

## vue组件间的数据通信方式有哪些

breforCreate() {
  vue.prototype.$bus = this
}

## 描述下vuex的工作流程

## 路由传参方式有哪些
query params

## 路由的跳转方式
<router-link />
router.push()

## 怎么能不存储路由的跳转
replace

## 缓存路由
<keep-alive :include="['News', 'Message']">
  <router-view></router-view>
</keep-alive>

## 路由切换时触发的钩子方法
activated() {}
deactivated() {}

## 路由守卫有哪些
全局前置/全局后置
独享路由守卫
组件内路由守卫






 