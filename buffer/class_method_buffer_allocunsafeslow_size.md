<!-- YAML
added: v5.10.0
-->

* `size` {Integer} The desired length of the new `Buffer`

Allocates a new *non-zero-filled* and non-pooled `Buffer` of `size` bytes. The
`size` must be less than or equal to the value of [`buffer.kMaxLength`].
Otherwise, a [`RangeError`] is thrown. A zero-length `Buffer` will be created if
`size <= 0`.

The underlying memory for `Buffer` instances created in this way is *not
initialized*. The contents of the newly created `Buffer` are unknown and
*may contain sensitive data*. Use [`buf.fill(0)`][`buf.fill()`] to initialize such
`Buffer` instances to zeroes.

When using [`Buffer.allocUnsafe()`] to allocate new `Buffer` instances,
allocations under 4KB are, by default, sliced from a single pre-allocated
`Buffer`. This allows applications to avoid the garbage collection overhead of
creating many individually allocated `Buffer` instances. This approach improves
both performance and memory usage by eliminating the need to track and cleanup as
many `Persistent` objects.

However, in the case where a developer may need to retain a small chunk of
memory from a pool for an indeterminate amount of time, it may be appropriate
to create an un-pooled `Buffer` instance using `Buffer.allocUnsafeSlow()` then
copy out the relevant bits.

Example:

```js
// Need to keep around a few small chunks of memory
const store = [];

socket.on('readable', () => {
  const data = socket.read();

  // Allocate for retained data
  const sb = Buffer.allocUnsafeSlow(10);

  // Copy the data into the new allocation
  data.copy(sb, 0, 0, 10);

  store.push(sb);
});
```

Use of `Buffer.allocUnsafeSlow()` should be used only as a last resort *after*
a developer has observed undue memory retention in their applications.

A `TypeError` will be thrown if `size` is not a number.

