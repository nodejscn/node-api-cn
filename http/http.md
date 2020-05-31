
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

若要使用 HTTP 服务器和客户端，则可以 `require('http')`。

Node.js 中的 HTTP 接口旨在支持许多传统上难以使用的协议的特性。
特别是，大块的（且可能是块编码的）消息。
接口永远不会缓冲整个请求或响应，所以用户可以流式地传输数据。

HTTP 消息头由类似如下的对象表示：

<!-- eslint-skip -->
```js
{ 'content-length': '123',
  'content-type': 'text/plain',
  'connection': 'keep-alive',
  'host': 'mysite.com',
  'accept': '*/*' }
```

键是小写的。
值还未被修改。

为了支持所有可能的 HTTP 应用程序，Node.js 的 HTTP API 都是非常底层的。
它仅进行流处理和消息解析。
它将消息解析为消息头和消息主体，但不会解析具体的消息头或消息主体。

有关如何处理重复的消息头，详见 [`message.headers`]。

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

