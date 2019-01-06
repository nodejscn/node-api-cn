
<!--type=misc-->

几乎所有的 Node.js 应用都在某种程度上使用了流。
下面是一个例子，使用流实现了一个 HTTP 服务器：

```js
const http = require('http');

const server = http.createServer((req, res) => {
  // req 是一个 http.IncomingMessage 实例，它是可读流。
  // res 是一个 http.ServerResponse 实例，它是可写流。

  let body = '';
  // 接收数据为 utf8 字符串，
  // 如果没有设置字符编码，则会接收到 Buffer 对象。
  req.setEncoding('utf8');

  // 如果添加了监听器，则可读流会触发 'data' 事件。
  req.on('data', (chunk) => {
    body += chunk;
  });

  // 'end' 事件表明整个请求体已被接收。 
  req.on('end', () => {
    try {
      const data = JSON.parse(body);
      // 响应信息给用户。
      res.write(typeof data);
      res.end();
    } catch (er) {
      // json 解析失败。
      res.statusCode = 400;
      return res.end(`错误: ${er.message}`);
    }
  });
});

server.listen(1337);

// $ curl localhost:1337 -d "{}"
// object
// $ curl localhost:1337 -d "\"foo\""
// string
// $ curl localhost:1337 -d "not json"
// 错误: Unexpected token o in JSON at position 1
```

[可写流]（比如例子中的 `res`）会暴露了一些方法，比如 `write()` 和 `end()` 用于写入数据到流。

当数据可以从流读取时，[可读流]会使用 [`EventEmitter`] API 来通知应用程序。
从流读取数据的方式有很多种。

[可写流]和[可读流]都通过多种方式使用 [`EventEmitter`] API 来通讯流的当前状态。

[`Duplex`] 流和 [`Transform`] 流都是可写又可读的。

对于只需写入数据到流或从流消费数据的应用程序，并不需要直接实现流的接口，通常也不需要调用 `require('stream')`。

对于需要实现新类型的流的开发者，可以参阅[用于实现流的API][API for Stream Implementers]章节。
