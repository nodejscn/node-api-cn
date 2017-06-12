<!-- YAML
added: v7.10.0
-->

* `obj` {Object} An object representing a collection of key-value pairs

Instantiate a new `URLSearchParams` object with a query hash map. The key and
value of each property of `obj` are always coerced to strings.

*Note*: Unlike [`querystring`][] module, duplicate keys in the form of array
values are not allowed. Arrays are stringified using [`array.toString()`][],
which simply joins all array elements with commas.

```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams({
  user: 'abc',
  query: ['first', 'second']
});
console.log(params.getAll('query'));
  // Prints [ 'first,second' ]
console.log(params.toString());
  // Prints 'user=abc&query=first%2Csecond'
```

