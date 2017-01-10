<!-- YAML
added: v0.11.3
-->

* `section` {String} A string identifying the portion of the application for
  which the `debuglog` function is being created.
* Returns: {Function} The logging function

The `util.debuglog()` method is used to create a function that conditionally
writes debug messages to `stderr` based on the existence of the `NODE_DEBUG`
environment variable.  If the `section` name appears within the value of that
environment variable, then the returned function operates similar to
[`console.error()`][].  If not, then the returned function is a no-op.

For example:

```js
const util = require('util');
const debuglog = util.debuglog('foo');

debuglog('hello from foo [%d]', 123);
```

If this program is run with `NODE_DEBUG=foo` in the environment, then
it will output something like:

```txt
FOO 3245: hello from foo [123]
```

where `3245` is the process id.  If it is not run with that
environment variable set, then it will not print anything.

Multiple comma-separated `section` names may be specified in the `NODE_DEBUG`
environment variable. For example: `NODE_DEBUG=fs,net,tls`.

