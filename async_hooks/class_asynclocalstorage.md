<!-- YAML
added: v13.10.0
-->

This class is used to create asynchronous state within callbacks and promise
chains. It allows storing data throughout the lifetime of a web request
or any other asynchronous duration. It is similar to thread-local storage
in other languages.

The following example uses `AsyncLocalStorage` to build a simple logger
that assigns IDs to incoming HTTP requests and includes them in messages
logged within each request.

```js
const http = require('http');
const { AsyncLocalStorage } = require('async_hooks');

const asyncLocalStorage = new AsyncLocalStorage();

function logWithId(msg) {
  const id = asyncLocalStorage.getStore();
  console.log(`${id !== undefined ? id : '-'}:`, msg);
}

let idSeq = 0;
http.createServer((req, res) => {
  asyncLocalStorage.run(idSeq++, () => {
    logWithId('start');
    // Imagine any chain of async operations here
    setImmediate(() => {
      logWithId('finish');
      res.end();
    });
  });
}).listen(8080);

http.get('http://localhost:8080');
http.get('http://localhost:8080');
// Prints:
//   0: start
//   1: start
//   0: finish
//   1: finish
```

When having multiple instances of `AsyncLocalStorage`, they are independent
from each other. It is safe to instantiate this class multiple times.

