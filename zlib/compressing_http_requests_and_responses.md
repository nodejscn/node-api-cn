
The `zlib` module can be used to implement support for the `gzip` and `deflate`
content-encoding mechanisms defined by
[HTTP](https://tools.ietf.org/html/rfc7230#section-4.2).

The HTTP [`Accept-Encoding`][] header is used within an http request to identify
the compression encodings accepted by the client. The [`Content-Encoding`][]
header is used to identify the compression encodings actually applied to a
message.

*Note*: the examples given below are drastically simplified to show
the basic concept.  Using `zlib` encoding can be expensive, and the results
ought to be cached.  See [Memory Usage Tuning][] for more information
on the speed/memory/compression tradeoffs involved in `zlib` usage.

```js
// client request example
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
    // or, just use zlib.createUnzip() to handle both cases
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
// server example
// Running a gzip operation on every request is quite expensive.
// It would be much more efficient to cache the compressed buffer.
const zlib = require('zlib');
const http = require('http');
const fs = require('fs');
http.createServer((request, response) => {
  const raw = fs.createReadStream('index.html');
  let acceptEncoding = request.headers['accept-encoding'];
  if (!acceptEncoding) {
    acceptEncoding = '';
  }

  // Note: This is not a conformant accept-encoding parser.
  // See http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3
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

By default, the `zlib` methods will throw an error when decompressing
truncated data. However, if it is known that the data is incomplete, or
the desire is to inspect only the beginning of a compressed file, it is
possible to suppress the default error handling by changing the flushing
method that is used to decompress the last chunk of input data:

```js
// This is a truncated version of the buffer from the above examples
const buffer = Buffer.from('eJzT0yMA', 'base64');

zlib.unzip(
  buffer,
  { finishFlush: zlib.constants.Z_SYNC_FLUSH },
  (err, buffer) => {
    if (!err) {
      console.log(buffer.toString());
    } else {
      // handle error
    }
  });
```

This will not change the behavior in other error-throwing situations, e.g.
when the input data has an invalid format. Using this method, it will not be
possible to determine whether the input ended prematurely or lacks the
integrity checks, making it necessary to manually check that the
decompressed result is valid.

