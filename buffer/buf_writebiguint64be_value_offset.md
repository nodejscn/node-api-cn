<!-- YAML
added:
 - v12.0.0
 - v10.20.0
changes:
  - version: v14.10.0
    pr-url: https://github.com/nodejs/node/pull/34960
    description: This function is also available as `buf.writeBigUint64BE()`.
-->

* `value` {bigint} 要写入 `buf` 的数值。
* `offset` {integer} 开始写入之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 8`。**默认值:** `0`。
* 返回: {integer} `offset` 加上已写入的字节数。

将 `value` 作为大端序写入到 `buf` 中指定的 `offset` 位置。

```js
const buf = Buffer.allocUnsafe(8);

buf.writeBigUInt64BE(0xdecafafecacefaden, 0);

console.log(buf);
// 打印: <Buffer de ca fa fe ca ce fa de>
```

