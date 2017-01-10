
A subclass of `Error` that indicates that a provided argument was not within the
set or range of acceptable values for a function; whether that is a numeric
range, or outside the set of options for a given function parameter.

For example:

```js
require('net').connect(-1);
  // throws RangeError, port should be > 0 && < 65536
```

Node.js will generate and throw `RangeError` instances *immediately* as a form
of argument validation.

