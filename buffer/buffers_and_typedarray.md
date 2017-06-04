<!-- YAML
changes:
  - version: v3.0.0
    pr-url: https://github.com/nodejs/node/pull/2002
    description: The `Buffer`s class now inherits from `Uint8Array`.
-->

`Buffer` 实例也是 [`Uint8Array`] 实例。
但是与 ECMAScript 2015 中的 TypedArray 规范还是有些微妙的不同。
例如，当 [`ArrayBuffer#slice()`] 创建一个切片的副本时，[`Buffer#slice()`] 的实现是在现有的 `Buffer` 上不经过拷贝直接进行创建，这也使得 [`Buffer#slice()`] 更高效。

遵循以下注意事项，也可以从一个 `Buffer` 创建一个新的 [`TypedArray`] 实例：

1. `Buffer` 对象的内存是拷贝到 [`TypedArray`] 的，而不是共享的。

2. `Buffer` 对象的内存是被解析为一个明确元素的数组，而不是一个目标类型的字节数组。
也就是说，`new Uint32Array(Buffer.from([1, 2, 3, 4]))` 会创建一个包含 `[1, 2, 3, 4]` 四个元素的 [`Uint32Array`]，而不是一个只包含一个元素 `[0x1020304]` 或 `[0x4030201]` 的 [`Uint32Array`] 。

也可以通过 TypeArray 对象的 `.buffer` 属性创建一个新建的且与 [`TypedArray`] 实例共享同一分配内存的 `Buffer` 。

例子：

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// 拷贝 `arr` 的内容
const buf1 = Buffer.from(arr);

// 与 `arr` 共享内存
const buf2 = Buffer.from(arr.buffer);

// 输出: <Buffer 88 a0>
console.log(buf1);

// 输出: <Buffer 88 13 a0 0f>
console.log(buf2);

arr[1] = 6000;

// 输出: <Buffer 88 a0>
console.log(buf1);

// 输出: <Buffer 88 13 70 17>
console.log(buf2);
```

注意，当使用 [`TypedArray`] 的 `.buffer` 创建 `Buffer` 时，也可以通过传入 `byteOffset` 和 `length` 参数只使用 [`ArrayBuffer`] 的一部分。

例子：

```js
const arr = new Uint16Array(20);
const buf = Buffer.from(arr.buffer, 0, 16);

// 输出: 16
console.log(buf.length);
```

`Buffer.from()` 和 [`TypedArray.from()`] 有着不同的签名与实现。
具体而言，[`TypedArray`] 的变种接受第二个参数，在类型数组的每个元素上调用一次映射函数：

* `TypedArray.from(source[, mapFn[, thisArg]])`

`Buffer.from()` 方法不支持使用映射函数：

* [`Buffer.from(array)`]
* [`Buffer.from(buffer)`]
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`]
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`]

