<!-- YAML
added: v0.7.11
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10236
    description: The elements of `list` can now be `Uint8Array`s.
-->

* `list` {Array} 要合并的 `Buffer` 或 [`Uint8Array`] 实例的数组
* `totalLength` {integer} 合并时 `list` 中 `Buffer` 实例的总长度
* 返回: {Buffer}

返回一个合并了 `list` 中所有 `Buffer` 实例的新建的 `Buffer` 。

如果 `list` 中没有元素、或 `totalLength` 为 0 ，则返回一个新建的长度为 0 的 `Buffer` 。

如果没有提供 `totalLength` ，则从 `list` 中的 `Buffer` 实例计算得到。
为了计算 `totalLength` 会导致需要执行额外的循环，所以提供明确的长度会运行更快。

如果提供了 `totalLength`，`totalLength` 必须是一个正整数。如果从 `list` 中计算得到的 `Buffer` 长度超过了 `totalLength`，则合并的结果将会被截断为 `totalLength` 的长度。

例子：从一个包含三个 `Buffer` 实例的数组创建为一个单一的 `Buffer`。

```js
const buf1 = Buffer.alloc(10);
const buf2 = Buffer.alloc(14);
const buf3 = Buffer.alloc(18);
const totalLength = buf1.length + buf2.length + buf3.length;

// 输出: 42
console.log(totalLength);

const bufA = Buffer.concat([buf1, buf2, buf3], totalLength);

// 输出: <Buffer 00 00 00 00 ...>
console.log(bufA);

// 输出: 42
console.log(bufA.length);
```
