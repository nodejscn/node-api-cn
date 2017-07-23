<!-- YAML
added: v0.1.94
-->

The `Hmac` Class is a utility for creating cryptographic HMAC digests. It can
be used in one of two ways:

- As a [stream][] that is both readable and writable, where data is written
  to produce a computed HMAC digest on the readable side, or
- Using the [`hmac.update()`][] and [`hmac.digest()`][] methods to produce the
  computed HMAC digest.

The [`crypto.createHmac()`][] method is used to create `Hmac` instances. `Hmac`
objects are not to be created directly using the `new` keyword.

Example: Using `Hmac` objects as streams:

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', 'a secret');

hmac.on('readable', () => {
  const data = hmac.read();
  if (data) {
    console.log(data.toString('hex'));
    // Prints:
    //   7fd04df92f636fd450bc841c9418e5825c17f33ad9c87c518115a45971f7f77e
  }
});

hmac.write('some data to hash');
hmac.end();
```

Example: Using `Hmac` and piped streams:

```js
const crypto = require('crypto');
const fs = require('fs');
const hmac = crypto.createHmac('sha256', 'a secret');

const input = fs.createReadStream('test.js');
input.pipe(hmac).pipe(process.stdout);
```

Example: Using the [`hmac.update()`][] and [`hmac.digest()`][] methods:

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', 'a secret');

hmac.update('some data to hash');
console.log(hmac.digest('hex'));
// Prints:
//   7fd04df92f636fd450bc841c9418e5825c17f33ad9c87c518115a45971f7f77e
```

