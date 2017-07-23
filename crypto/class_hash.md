<!-- YAML
added: v0.1.92
-->

The `Hash` class is a utility for creating hash digests of data. It can be
used in one of two ways:

- As a [stream][] that is both readable and writable, where data is written
  to produce a computed hash digest on the readable side, or
- Using the [`hash.update()`][] and [`hash.digest()`][] methods to produce the
  computed hash.

The [`crypto.createHash()`][] method is used to create `Hash` instances. `Hash`
objects are not to be created directly using the `new` keyword.

Example: Using `Hash` objects as streams:

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.on('readable', () => {
  const data = hash.read();
  if (data) {
    console.log(data.toString('hex'));
    // Prints:
    //   6a2da20943931e9834fc12cfe5bb47bbd9ae43489a30726962b576f4e3993e50
  }
});

hash.write('some data to hash');
hash.end();
```

Example: Using `Hash` and piped streams:

```js
const crypto = require('crypto');
const fs = require('fs');
const hash = crypto.createHash('sha256');

const input = fs.createReadStream('test.js');
input.pipe(hash).pipe(process.stdout);
```

Example: Using the [`hash.update()`][] and [`hash.digest()`][] methods:

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.update('some data to hash');
console.log(hash.digest('hex'));
// Prints:
//   6a2da20943931e9834fc12cfe5bb47bbd9ae43489a30726962b576f4e3993e50
```

