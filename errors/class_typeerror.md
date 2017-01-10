
A subclass of `Error` that indicates that a provided argument is not an
allowable type. For example, passing a function to a parameter which expects a
string would be considered a TypeError.

```js
require('url').parse(() => { });
  // throws TypeError, since it expected a string
```

Node.js will generate and throw `TypeError` instances *immediately* as a form
of argument validation.

