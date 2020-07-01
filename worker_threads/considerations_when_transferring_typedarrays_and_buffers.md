
All `TypedArray` and `Buffer` instances are views over an underlying
`ArrayBuffer`. That is, it is the `ArrayBuffer` that actually stores
the raw data while the `TypedArray` and `Buffer` objects provide a
way of viewing and manipulating the data. It is possible and common
for multiple views to be created over the same `ArrayBuffer` instance.
Great care must be taken when using a transfer list to transfer an
`ArrayBuffer` as doing so will cause all `TypedArray` and `Buffer`
instances that share that same `ArrayBuffer` to become unusable.

```js
const ab = new ArrayBuffer(10);

const u1 = new Uint8Array(ab);
const u2 = new Uint16Array(ab);

console.log(u2.length);  // prints 5

port.postMessage(u1, [u1.buffer]);

console.log(u2.length);  // prints 0
```

For `Buffer` instances, specifically, whether the underlying
`ArrayBuffer` can be transferred or cloned depends entirely on how
instances were created, which often cannot be reliably determined.

An `ArrayBuffer` can be marked with [`markAsUntransferable()`][] to indicate
that it should always be cloned and never transferred.

Depending on how a `Buffer` instance was created, it may or may
not own its underlying `ArrayBuffer`. An `ArrayBuffer` must not
be transferred unless it is known that the `Buffer` instance
owns it. In particular, for `Buffer`s created from the internal
`Buffer` pool (using, for instance `Buffer.from()` or `Buffer.alloc()`),
transferring them is not possible and they will always be cloned,
which sends a copy of the entire `Buffer` pool.
This behavior may come with unintended higher memory
usage and possible security concerns.

See [`Buffer.allocUnsafe()`][] for more details on `Buffer` pooling.

The `ArrayBuffer`s for `Buffer` instances created using
`Buffer.alloc()` or `Buffer.allocUnsafeSlow()` can always be
transferred but doing so will render all other existing views of
those `ArrayBuffer`s unusable.

