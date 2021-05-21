<!-- YAML
added: v13.1.0
-->

* `options` {Object} [`stream.transform` options][]
* Returns: {Hash}

Creates a new `Hash` object that contains a deep copy of the internal state
of the current `Hash` object.

The optional `options` argument controls stream behavior. For XOF hash
functions such as `'shake256'`, the `outputLength` option can be used to
specify the desired output length in bytes.

An error is thrown when an attempt is made to copy the `Hash` object after
its [`hash.digest()`][] method has been called.

```mjs
// Calculate a rolling hash.
const {
  createHash,
} = require('crypto');

const hash = createHash('sha256');

hash.update('one');
console.log(hash.copy().digest('hex'));

hash.update('two');
console.log(hash.copy().digest('hex'));

hash.update('three');
console.log(hash.copy().digest('hex'));

// Etc.
```

```cjs
// Calculate a rolling hash.
const {
  createHash,
} = require('crypto');

const hash = createHash('sha256');

hash.update('one');
console.log(hash.copy().digest('hex'));

hash.update('two');
console.log(hash.copy().digest('hex'));

hash.update('three');
console.log(hash.copy().digest('hex'));

// Etc.
```

