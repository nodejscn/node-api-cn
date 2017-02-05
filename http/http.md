
> 稳定性: 2 - 稳定的

使用 HTTP 服务器和客户端必须 `require('http')`。

Node.js 中的 HTTP 接口被设计为支持以往较难使用的协议的许多特性。
比如，大块编码的消息。
该接口从不缓存整个请求或响应，所以用户能够流化数据。

HTTP 消息头由类似以下的对象表示：

```js
{ 'content-length': '123',
  'content-type': 'text/plain',
  'connection': 'keep-alive',
  'host': 'mysite.com',
  'accept': '*/*' }
```

键名是小写的，值是不能修改的。

为了支持全部可能的 HTTP 应用，Node.js 的 HTTP API 是非常底层的。
它只涉及流处理和消息解析。
它把一个消息解析成头部和主体，但它不解析具体的头部或主体。

详见 [`message.headers`] 了解如何处理重复的头部。

收到的原始消息头保存在 `rawHeaders` 属性中，它是一个 `[key, value, key2, value2, ...]` 的数组。
例如，上面的消息头对象可能有一个类似以下的 `rawHeaders` 列表：

```js
[ 'ConTent-Length', '123456',
  'content-LENGTH', '123',
  'content-type', 'text/plain',
  'CONNECTION', 'keep-alive',
  'Host', 'mysite.com',
  'accepT', '*/*' ]
```

