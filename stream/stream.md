
> 稳定性: 2 - 稳定的

流（stream）在 Node.js 中是处理流数据的抽象接口（abstract interface）。
`stream` 模块提供了基础的 API 。使用这些 API 可以很容易地来构建实现流接口的对象。

Node.js 提供了多种流对象。 例如，
[HTTP 请求][http-incoming-message] 和 [`process.stdout`][]
就都是流的实例。

流可以是可读的、可写的，或是可读写的。所有的流都是
[`EventEmitter`][] 的实例。

`stream` 模块可以通过以下方式引入：

```js
const stream = require('stream');
```

尽管所有的 Node.js 用户都应该理解流的工作方式，这点很重要，
但是 `stream` 模块本身只对于那些需要创建新的流的实例的开发者最有用处。 对于主要是 *消费* 流的开发者来说，他们很少（如果有的话）需要直接使用
 `stream` 模块。
