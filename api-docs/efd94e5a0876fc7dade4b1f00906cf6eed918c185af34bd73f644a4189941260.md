
在压缩流上调用 [`.flush()`]() 方法将使 `zlib` 返回尽可能多的输出. 这可能是以压缩质量下降
为代价的，但是当需要尽快提供数据时，这可能是有用的

在以下的实例中,  `flush()` 方法用于将部分压缩过的 HTTP 响应返回给客户端:
```js
const zlib = require('zlib');
const http = require('http');

http.createServer((request, response) => {
  // 为了简单起见，省略了对 Accept-Encoding 的检测
  response.writeHead(200, { 'content-encoding': 'gzip' });
  const output = zlib.createGzip();
  output.pipe(response);

  setInterval(() => {
    output.write(`The current time is ${Date()}\n`, () => {
      // 数据已经传递给了 zlib，但压缩算法看能已经决定缓存数据以便得到更高的压缩效率。
      output.flush();
    });
  }, 1000);
}).listen(1337);
```
