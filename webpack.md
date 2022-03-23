# webpack性能优化

## 开发环境性能优化
* 优化打包构建速度
  * HMR
* 优化代码调试
  * source-map

## 生产环境性能优化
* 优化打包构建速度
  * oneOf
  * babel缓存，第二次打包会快一些
  * 多进程打包 thread-loader
  * externals （通过cdn连接的方式引入js）/ dll （配置好单独的文件，打包好的部分不再打包）
  
* 优化代码运行的性能
  * 缓存(hash-chunkhash-contenthash)
  * tree shaking （ES6模块，production开启）
  * code split (splitChunk)
  * 懒加载/预加载 （js 代码的异步加载）
  * pwa
  

### HMR
- 只会对更改的模块进行编译

### oneOf

### 多进程打包 thread-loader
- 进程开启是有时间的大概为600ms，进程通信也有时间开销
- 只有工作消耗时间比较长才需要多进程打包，不然会适得其反
- 给 babel-loader 使用（因为babel-loader，会做代码检查，编译比较耗时）

### tree shaking: 去除无用代码，减少代码体积
- 前提：1、必须使用ES6模块化 2、开启production环境
- 在package.json中配置
  - "sideEffects": false 所有代码都没有副作用（都可以进行tree shaking），问题是可能会把css、@babel/polyfiill文件干掉
  - "sideEffects": [".*css", "*.less"] 就不会误删
