
> Stability: 2 - Stable

A stream is an abstract interface for working with streaming data in Node.js.
The `stream` module provides a base API that makes it easy to build objects
that implement the stream interface.

There are many stream objects provided by Node.js. For instance, a
[request to an HTTP server][http-incoming-message] and [`process.stdout`][]
are both stream instances.

Streams can be readable, writable, or both. All streams are instances of
[`EventEmitter`][].

The `stream` module can be accessed using:

```js
const stream = require('stream');
```

While it is important for all Node.js users to understand how streams work,
the `stream` module itself is most useful for developers that are creating new
types of stream instances. Developer's who are primarily *consuming* stream
objects will rarely (if ever) have need to use the `stream` module directly.

