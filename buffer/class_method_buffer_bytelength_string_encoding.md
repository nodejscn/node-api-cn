<!-- YAML
added: v0.1.90
-->

* `string` {String | Buffer | TypedArray | DataView | ArrayBuffer} A value to
  calculate the length of
* `encoding` {String} If `string` is a string, this is its encoding.
  **Default:** `'utf8'`
* Returns: {Integer} The number of bytes contained within `string`

Returns the actual byte length of a string. This is not the same as
[`String.prototype.length`] since that returns the number of *characters* in
a string.

Example:

```js
const str = '\u00bd + \u00bc = \u00be';

// Prints: ½ + ¼ = ¾: 9 characters, 12 bytes
console.log(`${str}: ${str.length} characters, ` +
            `${Buffer.byteLength(str, 'utf8')} bytes`);
```

When `string` is a `Buffer`/[`DataView`]/[`TypedArray`]/[`ArrayBuffer`], the
actual byte length is returned.

Otherwise, converts to `String` and returns the byte length of string.

