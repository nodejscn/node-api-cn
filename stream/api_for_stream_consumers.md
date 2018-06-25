
<!--type=misc-->

几乎所有的 Node.js 应用，不管多么简单，都在某种程度上使用了流。
下面是在 Node.js 应用中使用流实现的一个简单的 HTTP 服务器：

```js
const http = require('http');

const server = http.createServer((req, res) => {
  // req 是一个 http.IncomingMessage 实例，它是可读流。
  // res 是一个 http.ServerResponse 实例，它是可写流。

  let body = '';
  // 接收数据为 utf8 字符串，
  // 如果没有设置字符编码，将接收到 Buffer 对象。
  req.setEncoding('utf8');

  // 如果添加了监听器，可读流会触发 'data' 事件。
  req.on('data', (chunk) => {
    body += chunk;
  });

  // 'end' 事件表明整个请求体已被接收。 
  req.on('end', () => {
    try {
      const data = JSON.parse(body);
      // 响应一些信息给用户。
      res.write(typeof data);
      res.end();
    } catch (er) {
      // json 数据解析失败。
      res.statusCode = 400;
      return res.end(`error: ${er.message}`);
    }
  });
});

server.listen(1337);

// $ curl localhost:1337 -d "{}"
// object
// $ curl localhost:1337 -d "\"foo\""
// string
// $ curl localhost:1337 -d "not json"
// error: Unexpected token o in JSON at position 1
```

[`Writable`] 流（比如例子中的 `res`）暴露了一些方法，比如 `write()` 和 `end()` 用于将数据写入到流中。

当流中的数据可以读取时，[`Readable`] 流使用 [`EventEmitter`] API 来通知应用。
这些数据可以使用多种方法从流中读取。

[`Writable`] 流和 [`Readable`] 流都通过多种方式使用 [`EventEmitter`] API 来通讯流的当前状态。

[`Duplex`] 流和 [`Transform`] 流都是可读可写的。

对于只是简单写入数据到流和从流中消费数据的应用来说，并不需要直接实现流接口，通常也不需要调用 `require('stream')`。

需要实现新类型的流的开发者可以参考[用于实现流的API][API for Stream Implementers] 的文档。
