`zlib` 可以用来实现对 [HTTP](https://tools.ietf.org/html/rfc7230#section-4.2) 中定义的 `gzip` 和 `deflate` 内容编码机制的支持。

HTTP 的 [`Accept-Encoding`][] 头字段用来标记客户端接受的压缩编码。
。

`注意`: 下面给出的示例大幅简化，用以展示了基本的概念。使用 `zlib` 编码成本会很高, 结果应该被缓存。关于 `zlib` 使用中有关速度/内存/压缩互相权衡的信息，查阅 [Memory Usage Tuning][]。

```js
// 客户端请求示例
const zlib = require('zlib');
const http = require('http');
const fs = require('fs');
const request = http.get({ host: 'example.com',
                           path: '/',
                           port: 80,
                           headers: { 'Accept-Encoding': 'gzip,deflate' } });
request.on('response', (response) => {
  const output = fs.createWriteStream('example.com_index.html');

  switch (response.headers['content-encoding']) {
    // 或者, 只是使用 zlib.createUnzip() 方法去处理这两种情况
    case 'gzip':
      response.pipe(zlib.createGunzip()).pipe(output);
      break;
    case 'deflate':
      response.pipe(zlib.createInflate()).pipe(output);
      break;
    default:
      response.pipe(output);
      break;
  }
});
```

```js
// 服务端示例
// 对每一个请求运行 gzip 操作的成本是十分高昂的.
// 缓存压缩缓冲区是更加高效的方式.
const zlib = require('zlib');
const http = require('http');
const fs = require('fs');
http.createServer((request, response) => {
  const raw = fs.createReadStream('index.html');
  let acceptEncoding = request.headers['accept-encoding'];
  if (!acceptEncoding) {
    acceptEncoding = '';
  }

  // 注意：这不是一个合适的 accept-encoding 解析器.
  // 查阅 http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3
  if (/\bdeflate\b/.test(acceptEncoding)) {
    response.writeHead(200, { 'Content-Encoding': 'deflate' });
    raw.pipe(zlib.createDeflate()).pipe(response);
  } else if (/\bgzip\b/.test(acceptEncoding)) {
    response.writeHead(200, { 'Content-Encoding': 'gzip' });
    raw.pipe(zlib.createGzip()).pipe(response);
  } else {
    response.writeHead(200, {});
    raw.pipe(response);
  }
}).listen(1337);
```

默认情况下, 当解压不完整的数据时 `zlib` 方法会抛出一个错误. 然而, 如果它已经知道数据是不完整的, 或者仅仅是为了检查已压缩文件的开头, 可以通过改变用来解压最后一个的输入数据块的刷新方法来避免默认的错误处理.

```js
// 这是一个上面例子中缓存区的不完整版本
const buffer = Buffer.from('eJzT0yMA', 'base64');

zlib.unzip(
  buffer,
  { finishFlush: zlib.constants.Z_SYNC_FLUSH },
  (err, buffer) => {
    if (!err) {
      console.log(buffer.toString());
    } else {
      // 错误处理
    }
  });
```

这不会改变其他抛出错误情况下的行为, 例如, 当输入内容的格式无效时. 使用这个方法, 无法确定输入是否过早结束, 或者缺乏完整性检查, 因此有必要人工检查解压结果是否有效.
