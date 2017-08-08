<!-- YAML
added: v7.1.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10236
    description: The `source` parameter can now be a `Uint8Array`.
-->

* `source` {Buffer|Uint8Array} 一个 `Buffer` 或 `Uint8Array` 实例
* `fromEnc` {string} 当前编码
* `toEnc` {string} 目标编码


将给定的 `Buffer` 或 `Uint8Array` 实例从一个字符编码重新编码到另一个字符。 返回一个新的Buffer实例。

如果 `fromEnc` 或 `toEnc` 指定的字符串编码无效，或者不允许从 `fromEnc` 转换为 `toEnc`，将抛出异常。

如果给定的字节序列不能在目标编码中充分表示，转码过程将使用替代字符。例如：

```js
const buffer = require('buffer');

const newBuf = buffer.transcode(Buffer.from('€'), 'utf8', 'ascii');
console.log(newBuf.toString('ascii'));
// 输出: '?'
```

因为欧元符号（`€`）不能在 US-ASCII 中表示，所以在转换 `Buffer` 的时候使用 `?` 代替。

注意 `buffer` 属性是通过 `require('buffer')` 返回的 `buffer` 模块，而不是全局 `Buffer` 或 `Buffer` 实例的属性。
