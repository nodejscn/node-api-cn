<!-- YAML
added: v0.1.94
-->

Instances of the `Decipher` class are used to decrypt data. The class can be
used in one of two ways:

- As a [stream][] that is both readable and writable, where plain encrypted
  data is written to produce unencrypted data on the readable side, or
- Using the [`decipher.update()`][] and [`decipher.final()`][] methods to
  produce the unencrypted data.

The [`crypto.createDecipher()`][] or [`crypto.createDecipheriv()`][] methods are
used to create `Decipher` instances. `Decipher` objects are not to be created
directly using the `new` keyword.

Example: Using `Decipher` objects as streams:

```js
const crypto = require('crypto');
const decipher = crypto.createDecipher('aes192', 'a password');

let decrypted = '';
decipher.on('readable', () => {
  const data = decipher.read();
  if (data)
    decrypted += data.toString('utf8');
});
decipher.on('end', () => {
  console.log(decrypted);
  // Prints: some clear text data
});

const encrypted =
    'ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504';
decipher.write(encrypted, 'hex');
decipher.end();
```

Example: Using `Decipher` and piped streams:

```js
const crypto = require('crypto');
const fs = require('fs');
const decipher = crypto.createDecipher('aes192', 'a password');

const input = fs.createReadStream('test.enc');
const output = fs.createWriteStream('test.js');

input.pipe(decipher).pipe(output);
```

Example: Using the [`decipher.update()`][] and [`decipher.final()`][] methods:

```js
const crypto = require('crypto');
const decipher = crypto.createDecipher('aes192', 'a password');

const encrypted =
    'ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504';
let decrypted = decipher.update(encrypted, 'hex', 'utf8');
decrypted += decipher.final('utf8');
console.log(decrypted);
// Prints: some clear text data
```

