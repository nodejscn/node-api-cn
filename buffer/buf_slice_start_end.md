<!-- YAML
added: v0.3.0
-->

* `start` {Integer} Where the new `Buffer` will start. **Default:** `0`
* `end` {Integer} Where the new `Buffer` will end (not inclusive).
  **Default:** [`buf.length`]
* Returns: {Buffer}

Returns a new `Buffer` that references the same memory as the original, but
offset and cropped by the `start` and `end` indices.

**Note that modifying the new `Buffer` slice will modify the memory in the
original `Buffer` because the allocated memory of the two objects overlap.**

Example: Create a `Buffer` with the ASCII alphabet, take a slice, and then modify
one byte from the original `Buffer`

```js
const buf1 = Buffer.allocUnsafe(26);

for (var i = 0 ; i < 26 ; i++) {
  // 97 is the decimal ASCII value for 'a'
  buf1[i] = i + 97;
}

const buf2 = buf1.slice(0, 3);

// Prints: abc
console.log(buf2.toString('ascii', 0, buf2.length));

buf1[0] = 33;

// Prints: !bc
console.log(buf2.toString('ascii', 0, buf2.length));
```

Specifying negative indexes causes the slice to be generated relative to the
end of `buf` rather than the beginning.

Examples:

```js
const buf = Buffer.from('buffer');

// Prints: buffe
// (Equivalent to buf.slice(0, 5))
console.log(buf.slice(-6, -1).toString());

// Prints: buff
// (Equivalent to buf.slice(0, 4))
console.log(buf.slice(-6, -2).toString());

// Prints: uff
// (Equivalent to buf.slice(1, 4))
console.log(buf.slice(-5, -2).toString());
```

