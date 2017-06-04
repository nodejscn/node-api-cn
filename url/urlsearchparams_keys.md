
* Returns: {Iterator}

Returns an ES6 Iterator over the names of each name-value pair.

```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams('foo=bar&foo=baz');
for (const name of params.keys()) {
  console.log(name);
}
  // Prints:
  // foo
  // foo
```

