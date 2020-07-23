<!-- YAML
added: v0.11.15
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->

* `offset` {integer} 开始读取之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 4`。**默认值:** `0`。
* 返回: {number}

从 `buf` 中指定的 `offset` 读取一个 32 位的小端序浮点值。

```js
const buf = Buffer.from([1, 2, 3, 4]);

console.log(buf.readFloatLE(0));
// 打印: 1.539989614439558e-36
console.log(buf.readFloatLE(1));
// 抛出异常 ERR_OUT_OF_RANGE。
```

