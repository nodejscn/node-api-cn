
It is possible for Node.js to be built without including support for the
`crypto` module. In such cases, calling `require('crypto')` will result in an
error being thrown.

```js
let crypto;
try {
  crypto = require('crypto');
} catch (err) {
  console.log('crypto support is disabled!');
}
```

