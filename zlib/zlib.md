
> Stability: 2 - Stable

The `zlib` module provides compression functionality implemented using Gzip and
Deflate/Inflate. It can be accessed using:

```js
const zlib = require('zlib');
```

Compressing or decompressing a stream (such as a file) can be accomplished by
piping the source stream data through a `zlib` stream into a destination stream:

```js
const gzip = zlib.createGzip();
const fs = require('fs');
const inp = fs.createReadStream('input.txt');
const out = fs.createWriteStream('input.txt.gz');

inp.pipe(gzip).pipe(out);
```

It is also possible to compress or decompress data in a single step:

```js
const input = '.................................';
zlib.deflate(input, (err, buffer) => {
  if (!err) {
    console.log(buffer.toString('base64'));
  } else {
    // handle error
  }
});

const buffer = Buffer.from('eJzT0yMAAGTvBe8=', 'base64');
zlib.unzip(buffer, (err, buffer) => {
  if (!err) {
    console.log(buffer.toString());
  } else {
    // handle error
  }
});
```

