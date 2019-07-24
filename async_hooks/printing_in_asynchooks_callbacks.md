
Because printing to the console is an asynchronous operation, `console.log()`
will cause the AsyncHooks callbacks to be called. Using `console.log()` or
similar asynchronous operations inside an AsyncHooks callback function will thus
cause an infinite recursion. An easy solution to this when debugging is to use a
synchronous logging operation such as `fs.writeFileSync(file, msg, flag)`.
This will print to the file and will not invoke AsyncHooks recursively because
it is synchronous.

```js
const fs = require('fs');
const util = require('util');

function debug(...args) {
  // use a function like this one when debugging inside an AsyncHooks callback
  fs.writeFileSync('log.out', `${util.format(...args)}\n`, { flag: 'a' });
}
```

If an asynchronous operation is needed for logging, it is possible to keep
track of what caused the asynchronous operation using the information
provided by AsyncHooks itself. The logging should then be skipped when
it was the logging itself that caused AsyncHooks callback to call. By
doing this the otherwise infinite recursion is broken.

