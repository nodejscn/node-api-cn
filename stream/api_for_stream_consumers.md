
<!--type=misc-->

Almost all Node.js applications, no matter how simple, use streams in some
manner. The following is an example of using streams in a Node.js application
that implements an HTTP server:

```js
const http = require('http');

const server = http.createServer( (req, res) => {
  // req is an http.IncomingMessage, which is a Readable Stream
  // res is an http.ServerResponse, which is a Writable Stream

  let body = '';
  // Get the data as utf8 strings.
  // If an encoding is not set, Buffer objects will be received.
  req.setEncoding('utf8');

  // Readable streams emit 'data' events once a listener is added
  req.on('data', (chunk) => {
    body += chunk;
  });

  // the end event indicates that the entire body has been received
  req.on('end', () => {
    try {
      const data = JSON.parse(body);
      // write back something interesting to the user:
      res.write(typeof data);
      res.end();
    } catch (er) {
      // uh oh!  bad json!
      res.statusCode = 400;
      return res.end(`error: ${er.message}`);
    }
  });
});

server.listen(1337);

// $ curl localhost:1337 -d '{}'
// object
// $ curl localhost:1337 -d '"foo"'
// string
// $ curl localhost:1337 -d 'not json'
// error: Unexpected token o
```

[Writable][] streams (such as `res` in the example) expose methods such as
`write()` and `end()` that are used to write data onto the stream.

[Readable][] streams use the [`EventEmitter`][] API for notifying application
code when data is available to be read off the stream. That available data can
be read from the stream in multiple ways.

Both [Writable][] and [Readable][] streams use the [`EventEmitter`][] API in
various ways to communicate the current state of the stream.

[Duplex][] and [Transform][] streams are both [Writable][] and [Readable][].

Applications that are either writing data to or consuming data from a stream
are not required to implement the stream interfaces directly and will generally
have no reason to call `require('stream')`.

Developers wishing to implement new types of streams should refer to the
section [API for Stream Implementers][].

