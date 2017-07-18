
在压缩流上调用 [`.flush()`]() 方法将使 `zlib` 返回尽可能多的输出. 这可能是以压缩质量下降
为代价的，但是当需要尽快提供数据时，这可能是有用的

在以下的实例中,  `flush()` 方法用于将部分压缩过的 HTTP 响应返回给客户端:
```js
const zlib = require('zlib');
const http = require('http');

http.createServer((request, response) => {
  // For the sake of simplicity, the Accept-Encoding checks are omitted.
  response.writeHead(200, { 'content-encoding': 'gzip' });
  const output = zlib.createGzip();
  output.pipe(response);

  setInterval(() => {
    output.write(`The current time is ${Date()}\n`, () => {
      // The data has been passed to zlib, but the compression algorithm may
      // have decided to buffer the data for more efficient compression.
      // Calling .flush() will make the data available as soon as the client
      // is ready to receive it.
      output.flush();
    });
  }, 1000);
}).listen(1337);
```

