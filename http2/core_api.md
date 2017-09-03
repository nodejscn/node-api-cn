
The Core API provides a low-level interface designed specifically around
support for HTTP/2 protocol features. It is specifically *not* designed for
compatibility with the existing [HTTP/1][] module API. However, the [Compatibility API][] is.

The following illustrates a simple, plain-text HTTP/2 server using the
Core API:

```js
const http2 = require('http2');

// Create a plain-text HTTP/2 server
const server = http2.createServer();

server.on('stream', (stream, headers) => {
  // stream is a Duplex
  stream.respond({
    'content-type': 'text/html',
    ':status': 200
  });
  stream.end('<h1>Hello World</h1>');
});

server.listen(80);
```

Note that the above example is an HTTP/2 server that does not support SSL.
This is significant as most browsers support HTTP/2 only with SSL.
To make the above server be able to serve content to browsers,
replace `http2.createServer()` with
`http2.createSecureServer({key: /* your SSL key */, cert: /* your SSL cert */})`.

The following illustrates an HTTP/2 client:

```js
const http2 = require('http2');

const client = http2.connect('http://localhost:80');

// req is a Duplex
const req = client.request({ ':path': '/' });

req.on('response', (headers) => {
  console.log(headers[':status']);
  console.log(headers['date']);
});

let data = '';
req.setEncoding('utf8');
req.on('data', (d) => data += d);
req.on('end', () => client.destroy());
req.end();
```

