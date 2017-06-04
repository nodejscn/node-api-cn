
* `fn` {Function} Function invoked for each name-value pair in the query.
* `thisArg` {Object} Object to be used as `this` value for when `fn` is called

Iterates over each name-value pair in the query and invokes the given function.

```js
const URL = require('url').URL;
const myURL = new URL('https://example.org/?a=b&c=d');
myURL.searchParams.forEach((value, name, searchParams) => {
  console.log(name, value, myURL.searchParams === searchParams);
});
  // Prints:
  // a b true
  // c d true
```

