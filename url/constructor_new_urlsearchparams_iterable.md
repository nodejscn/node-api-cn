<!-- YAML
added: v7.10.0
-->

* `iterable` {Iterable} An iterable object whose elements are key-value pairs

Instantiate a new `URLSearchParams` object with an iterable map in a way that
is similar to [`Map`][]'s constructor. `iterable` can be an Array or any
iterable object. That means `iterable` can be another `URLSearchParams`, in
which case the constructor will simply create a clone of the provided
`URLSearchParams`.  Elements of `iterable` are key-value pairs, and can
themselves be any iterable object.

Duplicate keys are allowed.

```js
const { URLSearchParams } = require('url');
let params;

// Using an array
params = new URLSearchParams([
  ['user', 'abc'],
  ['query', 'first'],
  ['query', 'second']
]);
console.log(params.toString());
  // Prints 'user=abc&query=first&query=second'

// Using a Map object
const map = new Map();
map.set('user', 'abc');
map.set('query', 'xyz');
params = new URLSearchParams(map);
console.log(params.toString());
  // Prints 'user=abc&query=xyz'

// Using a generator function
function* getQueryPairs() {
  yield ['user', 'abc'];
  yield ['query', 'first'];
  yield ['query', 'second'];
}
params = new URLSearchParams(getQueryPairs());
console.log(params.toString());
  // Prints 'user=abc&query=first&query=second'

// Each key-value pair must have exactly two elements
new URLSearchParams([
  ['user', 'abc', 'error']
]);
  // Throws TypeError [ERR_INVALID_TUPLE]:
  //        Each query pair must be an iterable [name, value] tuple
```

