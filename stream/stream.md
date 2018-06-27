
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

流（stream）是一种在 Node.js 中处理流式数据的抽象接口。
`stream` 模块提供了一些基础的 API，用于构建实现了流接口的对象。

Node.js 提供了多种流对象。 
例如，[发送到 HTTP 服务器的请求][http-incoming-message]和 [`process.stdout`] 都是流的实例。

流可以是可读的、可写的、或是可读写的。
所有的流都是 [`EventEmitter`] 的实例。

`stream` 模块可以通过以下方式使用：

```js
const stream = require('stream');
```

尽管理解流的工作方式很重要，但是 `stream` 模块本身主要用于开发者创建新类型的流实例。 
对于以消费流对象为主的开发者，极少需要直接使用 `stream` 模块。

