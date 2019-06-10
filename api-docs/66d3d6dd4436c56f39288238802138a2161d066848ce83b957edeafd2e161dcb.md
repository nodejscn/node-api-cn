<!-- YAML
changes:
  - version: v3.0.0
    pr-url: https://github.com/nodejs/node/pull/2002
    description: The `Buffer`s class now inherits from `Uint8Array`.
-->

`Buffer` 实例也是 [`Uint8Array`] 实例，但是与 [`TypedArray`] 有微小的不同。
例如，[`ArrayBuffer#slice()`] 会创建切片的拷贝，而 [`Buffer#slice()`][`buf.slice()`] 是在现有的 `Buffer` 上创建而不拷贝，这使得 [`Buffer#slice()`][`buf.slice()`] 效率更高。

也可以从一个 `Buffer` 创建新的 [`TypedArray`] 实例，但需要注意以下事项：

1. `Buffer` 对象的内存是被拷贝到 [`TypedArray`]，而不是共享。

2. `Buffer` 对象的内存是被解释为不同元素的数组，而不是目标类型的字节数组。 
也就是说，`new Uint32Array(Buffer.from([1, 2, 3, 4]))` 会创建一个带有 4 个元素 `[1, 2, 3, 4]` 的 [`Uint32Array`]，而不是带有单个元素 `[0x1020304]` 或 `[0x4030201]` 的 [`Uint32Array`]。

通过使用 `TypedArray` 对象的 `.buffer` 属性，可以创建一个与 [`TypedArray`] 实例共享相同内存的新 `Buffer`。 

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

当使用 [`TypedArray`] 的 `.buffer` 创建 `Buffer` 时，也可以通过传入 `byteOffset` 和 `length` 参数只使用 [`TypedArray`] 的一部分。

```js
const arr = new Uint16Array(20);
const buf = Buffer.from(arr.buffer, 0, 16);

console.log(buf.length);
// 打印: 16
```

`Buffer.from()` 与 [`TypedArray.from()`] 有着不同的实现。
具体来说，[`TypedArray`] 可以接受第二个参数作为映射函数，在类型数组的每个元素上调用：

* `TypedArray.from(source[, mapFn[, thisArg]])`

`Buffer.from()` 则不支持映射函数的使用：

* [`Buffer.from(array)`]
* [`Buffer.from(buffer)`]
* [`Buffer.from(arrayBuffer[, byteOffset[, length]])`][`Buffer.from(arrayBuf)`]
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`]

