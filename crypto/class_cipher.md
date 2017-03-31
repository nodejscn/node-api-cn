<!-- YAML
added: v0.1.94
-->

Instances of the `Cipher` class are used to encrypt data. The class can be
used in one of two ways:

- As a [stream][] that is both readable and writable, where plain unencrypted
  data is written to produce encrypted data on the readable side, or
- Using the [`cipher.update()`][] and [`cipher.final()`][] methods to produce
  the encrypted data.

The [`crypto.createCipher()`][] or [`crypto.createCipheriv()`][] methods are
used to create `Cipher` instances. `Cipher` objects are not to be created
directly using the `new` keyword.

Example: Using `Cipher` objects as streams:

```js
const crypto = require('crypto');
const cipher = crypto.createCipher('aes192', 'a password');

let encrypted = '';
cipher.on('readable', () => {
  const data = cipher.read();
  if (data)
    encrypted += data.toString('hex');
});
cipher.on('end', () => {
  console.log(encrypted);
  // Prints: ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504
});

cipher.write('some clear text data');
cipher.end();
```

Example: Using `Cipher` and piped streams:

```js
const crypto = require('crypto');
const fs = require('fs');
const cipher = crypto.createCipher('aes192', 'a password');

const input = fs.createReadStream('test.js');
const output = fs.createWriteStream('test.enc');

input.pipe(cipher).pipe(output);
```

Example: Using the [`cipher.update()`][] and [`cipher.final()`][] methods:

```js
const crypto = require('crypto');
const cipher = crypto.createCipher('aes192', 'a password');

let encrypted = cipher.update('some clear text data', 'utf8', 'hex');
encrypted += cipher.final('hex');
console.log(encrypted);
// Prints: ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504
```

