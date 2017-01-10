
> Stability: 2 - Stable

Prior to the introduction of [`TypedArray`] in ECMAScript 2015 (ES6), the
JavaScript language had no mechanism for reading or manipulating streams
of binary data. The `Buffer` class was introduced as part of the Node.js
API to make it possible to interact with octet streams in the context of things
like TCP streams and file system operations.

Now that [`TypedArray`] has been added in ES6, the `Buffer` class implements the
[`Uint8Array`] API in a manner that is more optimized and suitable for Node.js'
use cases.

Instances of the `Buffer` class are similar to arrays of integers but
correspond to fixed-sized, raw memory allocations outside the V8 heap.
The size of the `Buffer` is established when it is created and cannot be
resized.

The `Buffer` class is a global within Node.js, making it unlikely that one
would need to ever use `require('buffer').Buffer`.

Examples:

```js
// Creates a zero-filled Buffer of length 10.
const buf1 = Buffer.alloc(10);

// Creates a Buffer of length 10, filled with 0x1.
const buf2 = Buffer.alloc(10, 1);

// Creates an uninitialized buffer of length 10.
// This is faster than calling Buffer.alloc() but the returned
// Buffer instance might contain old data that needs to be
// overwritten using either fill() or write().
const buf3 = Buffer.allocUnsafe(10);

// Creates a Buffer containing [0x1, 0x2, 0x3].
const buf4 = Buffer.from([1, 2, 3]);

// Creates a Buffer containing ASCII bytes [0x74, 0x65, 0x73, 0x74].
const buf5 = Buffer.from('test');

// Creates a Buffer containing UTF-8 bytes [0x74, 0xc3, 0xa9, 0x73, 0x74].
const buf6 = Buffer.from('tést', 'utf8');
```

