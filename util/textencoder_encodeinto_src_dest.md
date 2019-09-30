
* `src` {string} The text to encode.
* `dest` {Uint8Array} The array to hold the encode result.
* Returns: {Object}
  * `read` {number} The read Unicode code units of src.
  * `written` {number} The written UTF-8 bytes of dest.

UTF-8 encodes the `src` string to the `dest` Uint8Array and returns an object
containing the read Unicode code units and written UTF-8 bytes.

```js
const encoder = new TextEncoder();
const src = 'this is some data';
const dest = new Uint8Array(10);
const { read, written } = encoder.encodeInto(src, dest);
```

