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

将 `value` 作为小端序写入到 `buf` 中指定的 `offset` 位置。
`value` 必须是 JavaScript 数值。
当 `value` 不是 JavaScript 数值时，行为是未定义的。

```js
const buf = Buffer.allocUnsafe(4);

buf.writeFloatLE(0xcafebabe, 0);

console.log(buf);
// 打印: <Buffer bb fe 4a 4f>
```

