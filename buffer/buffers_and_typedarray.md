
`Buffer` instances are also [`Uint8Array`] instances. However, there are subtle
incompatibilities with the TypedArray specification in ECMAScript 2015.
For example, while [`ArrayBuffer#slice()`] creates a copy of the slice, the
implementation of [`Buffer#slice()`][`buf.slice()`] creates a view over the
existing `Buffer` without copying, making [`Buffer#slice()`][`buf.slice()`] far
more efficient.

It is also possible to create new [`TypedArray`] instances from a `Buffer` with
the following caveats:

1. The `Buffer` object's memory is copied to the [`TypedArray`], not shared.

2. The `Buffer` object's memory is interpreted as an array of distinct
elements, and not as a byte array of the target type. That is,
`new Uint32Array(Buffer.from([1, 2, 3, 4]))` creates a 4-element [`Uint32Array`]
   with elements `[1, 2, 3, 4]`, not a [`Uint32Array`] with a single element
   `[0x1020304]` or `[0x4030201]`.

It is possible to create a new `Buffer` that shares the same allocated memory as
a [`TypedArray`] instance by using the TypeArray object's `.buffer` property.

Example:

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// Copies the contents of `arr`
const buf1 = Buffer.from(arr);

// Shares memory with `arr`
const buf2 = Buffer.from(arr.buffer);

// Prints: <Buffer 88 a0>
console.log(buf1);

// Prints: <Buffer 88 13 a0 0f>
console.log(buf2);

arr[1] = 6000;

// Prints: <Buffer 88 a0>
console.log(buf1);

// Prints: <Buffer 88 13 70 17>
console.log(buf2);
```

Note that when creating a `Buffer` using a [`TypedArray`]'s `.buffer`, it is
possible to use only a portion of the underlying [`ArrayBuffer`] by passing in
`byteOffset` and `length` parameters.

Example:

```js
const arr = new Uint16Array(20);
const buf = Buffer.from(arr.buffer, 0, 16);

// Prints: 16
console.log(buf.length);
```

The `Buffer.from()` and [`TypedArray.from()`] have different signatures and
implementations. Specifically, the [`TypedArray`] variants accept a second
argument that is a mapping function that is invoked on every element of the
typed array:

* `TypedArray.from(source[, mapFn[, thisArg]])`

The `Buffer.from()` method, however, does not support the use of a mapping
function:

* [`Buffer.from(array)`]
* [`Buffer.from(buffer)`]
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`]
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`]

