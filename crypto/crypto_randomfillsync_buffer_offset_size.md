<!-- YAML
added: v7.10.0
-->

* `buffer` {Buffer|Uint8Array} Must be supplied.
* `offset` {number} Defaults to `0`.
* `size` {number} Defaults to `buffer.length - offset`.

Synchronous version of [`crypto.randomFill()`][].

Returns `buffer`

```js
const buf = Buffer.alloc(10);
console.log(crypto.randomFillSync(buf).toString('hex'));

crypto.randomFillSync(buf, 5);
console.log(buf.toString('hex'));

// The above is equivalent to the following:
crypto.randomFillSync(buf, 5, 5);
console.log(buf.toString('hex'));
```

