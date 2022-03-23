## 三种情况

### 非跨域请求
1. 请求排队
2. DNS解析，解析域名对应的ip地址
3. 建立TCP连接（三次握手）
4. HTTP发送请求
5. 服务器端处理，并返回数据结构
6. 浏览器端，接受HTTP响应报文
7. 浏览器端处理响应的数据
8. 页面的绘制和渲染（dom树，cssom树，合并、布局、渲染）
9. 关闭TCP连接（四次挥手）

### 跨域简单请求
- 前6步同上，第7步浏览器端会拿到数据后，根据请求的header头发现是跨域请求，于是丢弃数据，不做响应

### 跨域复杂请求
- 会在上面的第1步前发送一个预校验的options请求，询问服务端是否可以发起跨域请求，得到肯定的回复才会发起接口调用


## 跨域请求的解决方案：
1. jsonp，只支持get请求（模拟创建script 标签）
2. nginx，反向代理
3. cors，需要服务端配置响应头，包括Access-Control-Allow-Origin、Access-Control-Allow-Methods、Access-Control-Allow-Headers等
4. iframe，可以使用window.postMessage