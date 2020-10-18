<!-- YAML
added: v0.3.0
changes:
  - version:
    - v7.1.0
    - v6.9.2
    pr-url: https://github.com/nodejs/node/pull/9341
    description: Coercing the offsets to integers now handles values outside
                 the 32-bit integer range properly.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/9101
    description: All offsets are now coerced to integers before doing any
                 calculations with them.
-->

* `start` {integer} 新 `Buffer` 开始的位置。**默认值:** `0`。
* `end` {integer} 新 `Buffer` 结束的位置（不包含）。**默认值:** [`buf.length`]。
* 返回: {Buffer}

返回一个新的 `Buffer`，它引用与原始的 Buffer 相同的内存，但是由 `start` 和 `end` 索引进行偏移和裁剪。

这与 `buf.subarray()` 的行为相同。

此方法与 `Uint8Array.prototype.slice()` 不兼容，后者是 `Buffer` 的超类。
若要复制切片，则使用 `Uint8Array.prototype.slice()`。

```js
const buf = Buffer.from('buffer');

const copiedBuf = Uint8Array.prototype.slice.call(buf);
copiedBuf[0]++;
console.log(copiedBuf.toString());
// 打印: cuffer

console.log(buf.toString());
// 打印: buffer
```

