<!-- YAML
added: v0.5.5
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->

* `offset` {integer} 开始读取之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 4`。**默认值:** `0`。
* 返回: {integer}

从 `buf` 中指定的 `offset` 读取一个有符号大端序的 32 位整数值。

从 `Buffer` 中读取的整数值会被解析为二进制补码值。

```js
const buf = Buffer.from([0, 0, 0, 5]);

console.log(buf.readInt32BE(0));
// 打印: 5
```

