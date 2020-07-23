<!-- YAML
changes:
  - version: v3.0.0
    pr-url: https://github.com/nodejs/node/pull/2002
    description: The `Buffer`s class now inherits from `Uint8Array`.
-->

`Buffer` 实例也是 JavaScript 的 [`Uint8Array`] 和 [`TypedArray`] 实例。
所有的 [`TypedArray`] 方法在 `Buffer` 上也可用。 
但是，`Buffer` 的 API 和 [`TypedArray`] 的 API 之间存在细微的不兼容。

主要表现在：

* [`TypedArray#slice()`] 会创建 `TypedArray` 的片段的拷贝，而 [`Buffer#slice()`][`buf.slice()`] 是在现有的 `Buffer` 上创建视图而不进行拷贝。 
  此行为可能产生意外，并且仅用于旧版的兼容性。 
  [`TypedArray#subarray()`] 可用于在 `Buffer` 和其他 `TypedArray` 上实现 [`Buffer#slice()`][`buf.slice()`] 的行为。
* [`buf.toString()`] 与它在 `TypedArray` 上的等价物并不兼容。
* 一些方法，例如 [`buf.indexOf()`]，支持额外的参数。

有两种方法可以从一个 `Buffer` 创建新的 [`TypedArray`] 实例：

* 将 `Buffer` 传给 [`TypedArray`] 的构造函数，则会拷贝 `Buffer` 的内容（会被解析为整数数组，而不是目标类型的字节序列）。 

```js
const buf = Buffer.from([1, 2, 3, 4]);
const uint32array = new Uint32Array(buf);

console.log(uint32array);

// 打印: Uint32Array(4) [ 1, 2, 3, 4 ]
```

* 传入 `Buffer` 底层的 [`ArrayBuffer`]，则会创建与 `Buffer` 共享其内存的 [`TypedArray`]：

```js
const buf = Buffer.from('hello', 'utf16le');
const uint16arr = new Uint16Array(
  buf.buffer,
  buf.byteOffset,
  buf.length / Uint16Array.BYTES_PER_ELEMENT);

console.log(uint16array);

// 打印: Uint16Array(5) [ 104, 101, 108, 108, 111 ]
```

也可以通过使用 `TypedArray` 对象的 `.buffer` 属性，以相同的方式来创建一个与 [`TypedArray`] 实例共享相同分配内存的新 `Buffer`。 
在这种情况下，[`Buffer.from()`][`Buffer.from(arrayBuf)`] 的行为类似于 `new Uint8Array()`。

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// 拷贝 `arr` 的内容。
const buf1 = Buffer.from(arr);

// 与 `arr` 共享内存。
const buf2 = Buffer.from(arr.buffer);

console.log(buf1);
// 打印: <Buffer 88 a0>
console.log(buf2);
// 打印: <Buffer 88 13 a0 0f>

arr[1] = 6000;

console.log(buf1);
// 打印: <Buffer 88 a0>
console.log(buf2);
// 打印: <Buffer 88 13 70 17>
```

当使用 [`TypedArray`] 的 `.buffer` 创建 `Buffer` 时，也可以通过传入 `byteOffset` 和 `length` 参数只使用底层 [`ArrayBuffer`] 的一部分。

```js
const arr = new Uint16Array(20);
const buf = Buffer.from(arr.buffer, 0, 16);

console.log(buf.length);
// 打印: 16
```

`Buffer.from()` 与 [`TypedArray.from()`] 有着不同的实现。
具体来说，[`TypedArray`] 可以接受第二个参数作为映射函数，在类型数组的每个元素上调用：

* `TypedArray.from(source[, mapFn[, thisArg]])`

`Buffer.from()` 方法则不支持映射函数的使用：

* [`Buffer.from(array)`][]
* [`Buffer.from(buffer)`][]
* [`Buffer.from(arrayBuffer[, byteOffset[, length]])`][`Buffer.from(arrayBuf)`]
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`]

