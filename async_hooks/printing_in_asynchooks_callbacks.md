
Because printing to the console is an asynchronous operation, `console.log()`
will cause the AsyncHooks callbacks to be called. Using `console.log()` or
similar asynchronous operations inside an AsyncHooks callback function will thus
cause an infinite recursion. An easily solution to this when debugging is
to use a synchronous logging operation such as `fs.writeSync(1, msg)`. This
will print to stdout because `1` is the file descriptor for stdout and will
not invoke AsyncHooks recursively because it is synchronous.

```js
const fs = require('fs');
const util = require('util');

function debug(...args) {
  // use a function like this one when debugging inside an AsyncHooks callback
  fs.writeSync(1, `${util.format(...args)}\n`);
}
```

If an asynchronous operation is needed for logging, it is possible to keep
track of what caused the asynchronous operation using the information
provided by AsyncHooks itself. The logging should then be skipped when
it was the logging itself that caused AsyncHooks callback to call. By
doing this the otherwise infinite recursion is broken.

