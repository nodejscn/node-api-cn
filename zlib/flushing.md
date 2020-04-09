
在压缩流上调用 [`.flush()`] 方法将使 `zlib` 返回尽可能多的输出。
这可能是以压缩质量下降为代价的，但是当需要尽快提供数据时，这可能是有用的。

在以下的实例中, `flush()` 方法用于将部分压缩过的 HTTP 响应返回给客户端：
```js
const zlib = require('zlib');
const http = require('http');
const { pipeline } = require('stream');

http.createServer((request, response) => {
  // 为了简单起见，省略了对 Accept-Encoding 的检测。
  response.writeHead(200, { 'content-encoding': 'gzip' });
  const output = zlib.createGzip();
  let i;

  pipeline(output, response, (err) => {
    if (err) {
      // 如果发生错误，则我们将会无能为力，
      // 因为服务器已经发送了 200 响应码，
      // 并且已经向客户端发送了一些数据。 
      // 我们能做的最好就是立即终止响应并记录错误。
      clearInterval(i);
      response.end();
      console.error('发生错误:', err);
    }
  });

  i = setInterval(() => {
    output.write(`The current time is ${Date()}\n`, () => {
      // 数据已经传递给了 zlib，但压缩算法看能已经决定缓存数据以便得到更高的压缩效率。
      // 一旦客户端准备接收数据，调用 .flush() 将会使数据可用。
      output.flush();
    });
  }, 1000);
}).listen(1337);
```

