<!-- YAML
added: v3.0.0
deprecated: v6.0.0
changes:
  - version: v7.2.1
    pr-url: https://github.com/nodejs/node/pull/9529
    description: Calling this constructor no longer emits a deprecation warning.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8169
    description: Calling this constructor emits a deprecation warning now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4682
    description: The `byteOffset` and `length` parameters are supported now.
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`] 代替。

* `arrayBuffer` {ArrayBuffer} 一个 [`ArrayBuffer`]，或 [`TypedArray`] 的 `.buffer` 属性
* `byteOffset` {integer} 开始拷贝的索引。 **默认：** `0`
* `length` {integer} 拷贝的字节数。**默认：** `arrayBuffer.length - byteOffset`

该方法将创建一个 [`ArrayBuffer`] 的视图，而不会复制底层内存。例如，当传入一个 [`TypedArray`] 实例的 `.buffer` 属性的引用时，这个新建的 `Buffer` 会像 [`TypedArray`] 那样共享同一段分配的内存。

可选的 `byteOffset` 和 `length` 参数指定将与 `Buffer` 共享的 `arrayBuffer` 的内存范围。

例子:

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// 与 `arr` 共享内存
const buf = new Buffer(arr.buffer);

// 输出: <Buffer 88 13 a0 0f>
console.log(buf);

// 改变原始的 Uint16Array 也将改变 Buffer
arr[1] = 6000;

// 输出: <Buffer 88 13 70 17>
console.log(buf);
```
