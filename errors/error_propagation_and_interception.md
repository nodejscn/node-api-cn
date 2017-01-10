
<!--type=misc-->

Node.js supports several mechanisms for propagating and handling errors that
occur while an application is running. How these errors are reported and
handled depends entirely on the type of Error and the style of the API that is
called.

All JavaScript errors are handled as exceptions that *immediately* generate
and throw an error using the standard JavaScript `throw` mechanism. These
are handled using the [`try / catch` construct][try-catch] provided by the JavaScript
language.

```js
// Throws with a ReferenceError because z is undefined
try {
  const m = 1;
  const n = m + z;
} catch (err) {
  // Handle the error here.
}
```

Any use of the JavaScript `throw` mechanism will raise an exception that
*must* be handled using `try / catch` or the Node.js process will exit
immediately.

With few exceptions, _Synchronous_ APIs (any blocking method that does not
accept a `callback` function, such as [`fs.readFileSync`][]), will use `throw`
to report errors.

Errors that occur within _Asynchronous APIs_ may be reported in multiple ways:

- Most asynchronous methods that accept a `callback` function will accept an
  `Error` object passed as the first argument to that function. If that first
  argument is not `null` and is an instance of `Error`, then an error occurred
  that should be handled.

  ```js
  const fs = require('fs');
  fs.readFile('a file that does not exist', (err, data) => {
    if (err) {
      console.error('There was an error reading the file!', err);
      return;
    }
    // Otherwise handle the data
  });
  ```
- When an asynchronous method is called on an object that is an `EventEmitter`,
  errors can be routed to that object's `'error'` event.

  ```js
  const net = require('net');
  const connection = net.connect('localhost');

  // Adding an 'error' event handler to a stream:
  connection.on('error', (err) => {
    // If the connection is reset by the server, or if it can't
    // connect at all, or on any sort of error encountered by
    // the connection, the error will be sent here.
    console.error(err);
  });

  connection.pipe(process.stdout);
  ```

- A handful of typically asynchronous methods in the Node.js API may still
  use the `throw` mechanism to raise exceptions that must be handled using
  `try / catch`. There is no comprehensive list of such methods; please
  refer to the documentation of each method to determine the appropriate
  error handling mechanism required.

The use of the `'error'` event mechanism is most common for [stream-based][]
and [event emitter-based][] APIs, which themselves represent a series of
asynchronous operations over time (as opposed to a single operation that may
pass or fail).

For *all* `EventEmitter` objects, if an `'error'` event handler is not
provided, the error will be thrown, causing the Node.js process to report an
unhandled exception and  crash unless either: The [`domain`][domains] module is used
appropriately or a handler has been registered for the
[`process.on('uncaughtException')`][] event.

```js
const EventEmitter = require('events');
const ee = new EventEmitter();

setImmediate(() => {
  // This will crash the process because no 'error' event
  // handler has been added.
  ee.emit('error', new Error('This will crash'));
});
```

Errors generated in this way *cannot* be intercepted using `try / catch` as
they are thrown *after* the calling code has already exited.

Developers must refer to the documentation for each method to determine
exactly how errors raised by those methods are propagated.

