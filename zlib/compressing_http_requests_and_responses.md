
`zlib` 模块可以用来实现对 [HTTP] 中定义的 `gzip` 和 `deflate` 内容编码机制的支持。

HTTP 的 [`Accept-Encoding`] 消息头用来标记客户端接受的压缩编码。
[`Content-Encoding`] 消息头用于标识实际应用于消息的压缩编码。

下面给出的示例大幅简化，用以展示了基本的概念。
使用 `zlib` 编码成本会很高, 结果应该被缓存。
关于 `zlib` 使用中有关速度/内存/压缩互相权衡的信息，查阅[内存使用的调整][Memory Usage Tuning]。

```js
// 客户端请求示例。
const zlib = require('zlib');
const http = require('http');
const fs = require('fs');
const { pipeline } = require('stream');

const request = http.get({ host: 'example.com',
                           path: '/',
                           port: 80,
                           headers: { 'Accept-Encoding': 'br,gzip,deflate' } });
request.on('response', (response) => {
  const output = fs.createWriteStream('example.com_index.html');

  const onError = (err) => {
    if (err) {
      console.error('发生错误:', err);
      process.exitCode = 1;
    }
  };

  switch (response.headers['content-encoding']) {
    case 'br':
      pipeline(response, zlib.createBrotliDecompress(), output, onError);
      break;
    // 或者, 只是使用 zlib.createUnzip() 方法去处理这两种情况：
    case 'gzip':
      pipeline(response, zlib.createGunzip(), output, onError);
      break;
    case 'deflate':
      pipeline(response, zlib.createInflate(), outout, onError);
      break;
    default:
      pipeline(response, output, onError);
      break;
  }
});
```

```js
// 服务端示例。
// 对每一个请求运行 gzip 操作的成本是十分高昂的。
// 缓存已压缩的 buffer 是更加高效的方式。
const zlib = require('zlib');
const http = require('http');
const fs = require('fs');
const { pipeline } = require('stream');

http.createServer((request, response) => {
  const raw = fs.createReadStream('index.html');
  // 存储资源的压缩版本和未压缩版本。
  response.setHeader('Vary', 'Accept-Encoding');
  let acceptEncoding = request.headers['accept-encoding'];
  if (!acceptEncoding) {
    acceptEncoding = '';
  }

  const onError = (err) => {
    if (err) {
      // 如果发生错误，则我们将会无能为力，
      // 因为服务器已经发送了 200 响应码，
      // 并且已经向客户端发送了一些数据。 
      // 我们能做的最好就是立即终止响应并记录错误。
      response.end();
      console.error('发生错误:', err);
    }
  };

  // 注意：这不是一个合适的 accept-encoding 解析器。
  // 查阅 https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3
  if (/\bdeflate\b/.test(acceptEncoding)) {
    response.writeHead(200, { 'Content-Encoding': 'deflate' });
    pipeline(raw, zlib.createDeflate(), response, onError);
  } else if (/\bgzip\b/.test(acceptEncoding)) {
    response.writeHead(200, { 'Content-Encoding': 'gzip' });
    pipeline(raw, zlib.createGzip(), response, onError);
  } else if (/\bbr\b/.test(acceptEncoding)) {
    response.writeHead(200, { 'Content-Encoding': 'br' });
    pipeline(raw, zlib.createBrotliCompress(), response, onError);
  } else {
    response.writeHead(200, {});
    pipeline(raw, response, onError);
  }
}).listen(1337);
```

默认情况下，当解压不完整的数据时 `zlib` 方法会抛出一个错误。
然而，如果它已经知道数据是不完整的，或者仅仅是为了检查已压缩文件的开头，可以通过改变用来解压最后一个的输入数据块的刷新方法来避免默认的错误处理：

```js
// 这是一个上面例子中 buffer 的不完整版本。
const buffer = Buffer.from('eJzT0yMA', 'base64');

zlib.unzip(
  buffer,
  // 对于 Brotli，等效的是 zlib.constants.BROTLI_OPERATION_FLUSH。
  { finishFlush: zlib.constants.Z_SYNC_FLUSH },
  (err, buffer) => {
    if (err) {
      console.error('发生错误:', err);
      process.exitCode = 1;
    }
    console.log(buffer.toString());
  });
```

这不会改变其他抛出错误情况下的行为，例如，当输入内容的格式无效时。
使用这个方法，无法确定输入是否过早结束，或者缺乏完整性检查，因此有必要人工检查解压结果是否有效。

