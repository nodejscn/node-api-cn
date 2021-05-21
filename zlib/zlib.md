
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!-- source_link=lib/zlib.js -->

`zlib` 模块提供了使用 Gzip、Deflate/Inflate、和 Brotli 实现的压缩功能。

要访问它：

```js
const zlib = require('zlib');
```

压缩和解压缩是围绕 Node.js 的[流 API][Streams API] 构建的。

压缩或者解压缩一个流（例如一个文件）可以被通过将源流用管道通过 `zlib` `Transform` 流输送到一个目标流中来完成。

```js
const { createGzip } = require('zlib');
const { pipeline } = require('stream');
const {
  createReadStream,
  createWriteStream
} = require('fs');

const gzip = createGzip();
const source = createReadStream('input.txt');
const destination = createWriteStream('input.txt.gz');

pipeline(source, gzip, destination, (err) => {
  if (err) {
    console.error('发生一个错误:', err);
    process.exitCode = 1;
  }
});

// 或者 Promise 化

const { promisify } = require('util');
const pipe = promisify(pipeline);

async function do_gzip(input, output) {
  const gzip = createGzip();
  const source = createReadStream(input);
  const destination = createWriteStream(output);
  await pipe(source, gzip, destination);
}

do_gzip('input.txt', 'input.txt.gz')
  .catch((err) => {
    console.error('发生一个错误:', err);
    process.exitCode = 1;
  });
```

也可以在一个步骤中压缩或者解压缩数据：

```js
const { deflate, unzip } = require('zlib');

const input = '.................................';
deflate(input, (err, buffer) => {
  if (err) {
    console.error('发生一个错误:', err);
    process.exitCode = 1;
  }
  console.log(buffer.toString('base64'));
});

const buffer = Buffer.from('eJzT0yMAAGTvBe8=', 'base64');
unzip(buffer, (err, buffer) => {
  if (err) {
    console.error('发生一个错误:', err);
    process.exitCode = 1;
  }
  console.log(buffer.toString());
});

// 或者 Promise 化

const { promisify } = require('util');
const do_unzip = promisify(unzip);

do_unzip(buffer)
  .then((buf) => console.log(buf.toString()))
  .catch((err) => {
    console.error('发生一个错误:', err);
    process.exitCode = 1;
  });
```

