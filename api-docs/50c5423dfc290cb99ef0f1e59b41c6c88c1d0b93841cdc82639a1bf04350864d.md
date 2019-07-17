<!-- YAML
added: v0.11.15
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->


* `value` {number} 要写入 `buf` 的数值。
* `offset` {integer} 开始写入之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 4`。**默认值:** `0`。
* 返回: {integer} `offset` 加上已写入的字节数。

用指定的字节序格式（`writeFloatBE()` 写入大端序，`writeFloatLE()` 写入小端序）将 `value` 写入到 `buf` 中指定的 `offset` 位置。
`value` 必须是 32 位浮点值。
当 `value` 不是 32 位浮点值时，行为是未定义的。

```js
const buf = Buffer.allocUnsafe(4);

buf.writeFloatBE(0xcafebabe, 0);

console.log(buf);
// 打印: <Buffer 4f 4a fe bb>

buf.writeFloatLE(0xcafebabe, 0);

console.log(buf);
// 打印: <Buffer bb fe 4a 4f>
```

