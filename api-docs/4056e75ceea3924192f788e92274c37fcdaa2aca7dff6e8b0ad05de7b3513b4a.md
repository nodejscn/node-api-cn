<!-- YAML
added:
  - v7.10.0
  - v6.13.0
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15231
    description: The `buffer` argument may be any `TypedArray` or `DataView`.
-->

* `buffer` {Buffer|TypedArray|DataView} Must be supplied.
* `offset` {number} **Default:** `0`
* `size` {number} **Default:** `buffer.length - offset`
* Returns: {Buffer|TypedArray|DataView} The object passed as `buffer` argument.

Synchronous version of [`crypto.randomFill()`][].

```js
const buf = Buffer.alloc(10);
console.log(crypto.randomFillSync(buf).toString('hex'));

crypto.randomFillSync(buf, 5);
console.log(buf.toString('hex'));

// The above is equivalent to the following:
crypto.randomFillSync(buf, 5, 5);
console.log(buf.toString('hex'));
```

Any `TypedArray` or `DataView` instance may be passed as `buffer`.

```js
const a = new Uint32Array(10);
console.log(Buffer.from(crypto.randomFillSync(a).buffer,
                        a.byteOffset, a.byteLength).toString('hex'));

const b = new Float64Array(10);
console.log(Buffer.from(crypto.randomFillSync(b).buffer,
                        b.byteOffset, b.byteLength).toString('hex'));

const c = new DataView(new ArrayBuffer(10));
console.log(Buffer.from(crypto.randomFillSync(c).buffer,
                        c.byteOffset, c.byteLength).toString('hex'));
```

