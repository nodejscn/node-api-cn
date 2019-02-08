
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

要使用 HTTP 服务器和客户端，必须 `require('http')`。

Node.js 中的 HTTP 接口旨在支持传统上难以使用的协议的许多特性。
特别是，大块的、可能块编码的消息。
接口永远不会缓冲整个请求或响应，用户能够流式传输数据。

HTTP 消息头由如下对象表示：

<!-- eslint-skip -->
```js
{ 'content-length': '123',
  'content-type': 'text/plain',
  'connection': 'keep-alive',
  'host': 'mysite.com',
  'accept': '*/*' }
```

键是小写的。值不能被修改。

为了支持所有可能的 HTTP 应用程序，Node.js 的 HTTP API 都非常底层。
它仅进行流处理和消息解析。
它将消息解析为消息头和消息主体，但不会解析具体的消息头或消息主体。

有关如何处理重复消息头的详细信息，参阅 [`message.headers`]。

接收到的原始消息头保存在 `rawHeaders` 属性中，该属性是 `[key, value, key2, value2, ...]` 的数组。
例如，上面的消息头对象可能具有的 `rawHeaders` 列表如下所示：

<!-- eslint-disable semi -->
```js
[ 'ConTent-Length', '123456',
  'content-LENGTH', '123',
  'content-type', 'text/plain',
  'CONNECTION', 'keep-alive',
  'Host', 'mysite.com',
  'accepT', '*/*' ]
```

