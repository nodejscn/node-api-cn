
> Stability: 2 - Stable

<!--name=fs-->

File I/O is provided by simple wrappers around standard POSIX functions.  To
use this module do `require('fs')`. All the methods have asynchronous and
synchronous forms.

The asynchronous form always takes a completion callback as its last argument.
The arguments passed to the completion callback depend on the method, but the
first argument is always reserved for an exception. If the operation was
completed successfully, then the first argument will be `null` or `undefined`.

When using the synchronous form any exceptions are immediately thrown.
Exceptions may be handled using `try`/`catch`, or they may be allowed to
bubble up.

Here is an example of the asynchronous version:

```js
const fs = require('fs');

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('successfully deleted /tmp/hello');
});
```

Here is the synchronous version:

```js
const fs = require('fs');

fs.unlinkSync('/tmp/hello');
console.log('successfully deleted /tmp/hello');
```

With the asynchronous methods there is no guaranteed ordering. So the
following is prone to error:

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  console.log('renamed complete');
});
fs.stat('/tmp/world', (err, stats) => {
  if (err) throw err;
  console.log(`stats: ${JSON.stringify(stats)}`);
});
```

It could be that `fs.stat` is executed before `fs.rename`.
The correct way to do this is to chain the callbacks.

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`stats: ${JSON.stringify(stats)}`);
  });
});
```

In busy processes, the programmer is _strongly encouraged_ to use the
asynchronous versions of these calls. The synchronous versions will block
the entire process until they complete--halting all connections.

The relative path to a filename can be used. Remember, however, that this path
will be relative to `process.cwd()`.

While it is not recommended, most fs functions allow the callback argument to
be omitted, in which case a default callback is used that rethrows errors. To
get a trace to the original call site, set the `NODE_DEBUG` environment
variable:

*Note*: Omitting the callback function on asynchronous fs functions is
deprecated and may result in an error being thrown in the future.

```txt
$ cat script.js
function bad() {
  require('fs').readFile('/');
}
bad();

$ env NODE_DEBUG=fs node script.js
fs.js:88
        throw backtrace;
        ^
Error: EISDIR: illegal operation on a directory, read
    <stack trace.>
```

*Note:* On Windows Node.js follows the concept of per-drive working directory.
This behavior can be observed when using a drive path without a backslash. For
example `fs.readdirSync('c:\\')` can potentially return a different result than
`fs.readdirSync('c:')`. For more information, see
[this MSDN page][MSDN-Rel-Path].

