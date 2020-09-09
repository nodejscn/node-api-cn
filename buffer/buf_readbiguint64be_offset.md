<!-- YAML
added:
 - v12.0.0
 - v10.20.0
changes:
  - version: v14.10.0
    pr-url: https://github.com/nodejs/node/pull/34960
    description: This function is also available as `buf.readBigUint64BE()`.
-->

* `offset` {integer} 开始读取之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 8`。**默认值:** `0`。
* 返回: {bigint}

从 `buf` 中指定的 `offset` 读取一个无符号大端序的 64 位整数值。

```js
const buf = Buffer.from([0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff]);

console.log(buf.readBigUInt64BE(0));
// 打印: 4294967295n
```

