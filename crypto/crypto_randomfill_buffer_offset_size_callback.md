<!-- YAML
added: v7.10.0
-->

* `buffer` {Buffer|Uint8Array} Must be supplied.
* `offset` {number} Defaults to `0`.
* `size` {number} Defaults to `buffer.length - offset`.
* `callback` {Function} `function(err, buf) {}`.

This function is similar to [`crypto.randomBytes()`][] but requires the first
argument to be a [`Buffer`][] that will be filled. It also
requires that a callback is passed in.

If the `callback` function is not provided, an error will be thrown.

```js
const buf = Buffer.alloc(10);
crypto.randomFill(buf, (err, buf) => {
  if (err) throw err;
  console.log(buf.toString('hex'));
});

crypto.randomFill(buf, 5, (err, buf) => {
  if (err) throw err;
  console.log(buf.toString('hex'));
});

// The above is equivalent to the following:
crypto.randomFill(buf, 5, 5, (err, buf) => {
  if (err) throw err;
  console.log(buf.toString('hex'));
});
```

