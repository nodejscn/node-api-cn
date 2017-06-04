
<!--type=misc-->

几乎所有的 Node.js 应用，不管多么简单，都在某种程度上使用了流。
下面是在 Node.js 应用中使用流实现的一个简单的 HTTP 服务器：

```js
const http = require('http');

const server = http.createServer((req, res) => {
  // req 是 http.IncomingMessage 的实例，这是一个 Readable Stream
  // res 是 http.ServerResponse 的实例，这是一个 Writable Stream

  let body = '';
  // 接收数据为 utf8 字符串，
  // 如果没有设置字符编码，将接收到 Buffer 对象。
  req.setEncoding('utf8');

  // 如果监听了 'data' 事件，Readable streams 触发 'data' 事件 
  req.on('data', (chunk) => {
    body += chunk;
  });

  // end 事件表明整个 body 都接收完毕了 
  req.on('end', () => {
    try {
      const data = JSON.parse(body);
      // 发送一些信息给用户
      res.write(typeof data);
      res.end();
    } catch (er) {
      // json 数据解析失败 
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

[Writable][] 流 (比如例子中的 `res`) 暴露了一些方法，比如
`write()` 和 `end()` 。这些方法可以将数据写入到流中。

当流中的数据可以读取时，[Readable][] 流使用 [`EventEmitter`][] API 来通知应用。
这些数据可以使用多种方法从流中读取。

[Writable][] 和 [Readable][] 流都使用了 [`EventEmitter`][] API ，通过多种方式，
与流的当前状态进行交互。

[Duplex][] 和 [Transform][] 都是同时满足 [Writable][] 和 [Readable][] 。

对于只是简单写入数据到流和从流中消费数据的应用来说，
不要求直接实现流接口，通常也不需要调用 `require('stream')`。

需要实现两种类型流的开发者可以参考 [API for Stream Implementers][]。
