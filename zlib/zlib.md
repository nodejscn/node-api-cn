
> Stability: 2 - Stable

`zlib`模块提供通过 Gzip 和 Deflate/Inflate 实现的压缩功能，可以通过这样使用它：

```js
const zlib = require('zlib');
```

压缩或者解压数据流(例如一个文件)通过`zlib`流将源数据流传输到目标流中来完成。

```js
const gzip = zlib.createGzip();
const fs = require('fs');
const inp = fs.createReadStream('input.txt');
const out = fs.createWriteStream('input.txt.gz');

inp.pipe(gzip).pipe(out);
```

数据的压缩或解压缩也可以只用一个步骤完成：

```js
const input = '.................................';
zlib.deflate(input, (err, buffer) => {
  if (!err) {
    console.log(buffer.toString('base64'));
  } else {
    // 错误处理
  }
});

const buffer = Buffer.from('eJzT0yMAAGTvBe8=', 'base64');
zlib.unzip(buffer, (err, buffer) => {
  if (!err) {
    console.log(buffer.toString());
  } else {
    // 错误处理
  }
});
```
