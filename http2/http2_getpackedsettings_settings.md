<!-- YAML
added: v8.4.0
-->

* `settings` {[Settings Object][]}
* Returns: {Buffer}

Returns a `Buffer` instance containing serialized representation of the given
HTTP/2 settings as specified in the [HTTP/2][] specification. This is intended
for use with the `HTTP2-Settings` header field.

```js
const http2 = require('http2');

const packed = http2.getPackedSettings({ enablePush: false });

console.log(packed.toString('base64'));
// Prints: AAIAAAAA
```

