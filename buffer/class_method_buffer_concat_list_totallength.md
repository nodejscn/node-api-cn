<!-- YAML
added: v0.7.11
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10236
    description: The elements of `list` can now be `Uint8Array`s.
-->

* `list` {Buffer[] | Uint8Array[]} 要合并的 `Buffer` 数组或 [`Uint8Array`] 数组。
* `totalLength` {integer} 合并后 `list` 中的 `Buffer` 实例的总长度。
* 返回: {Buffer}

返回一个合并了 `list` 中所有 `Buffer` 实例的新 `Buffer`。

如果 `list` 中没有元素、或 `totalLength` 为 0，则返回一个长度为 0 的 `Buffer`。

如果没有提供 `totalLength`，则通过将 `list` 中的 `Buffer` 实例的长度相加来计算得出。

如果提供了 `totalLength`，则会强制转换为无符号整数。
如果 `list` 中的 `Buffer` 合并后的总长度大于 `totalLength`，则结果会被截断到 `totalLength` 的长度。

```js
// 用含有三个 `Buffer` 实例的数组创建一个单一的 `Buffer`。

const buf1 = Buffer.alloc(10);
const buf2 = Buffer.alloc(14);
const buf3 = Buffer.alloc(18);
const totalLength = buf1.length + buf2.length + buf3.length;

console.log(totalLength);
// 打印: 42

const bufA = Buffer.concat([buf1, buf2, buf3], totalLength);

console.log(bufA);
// 打印: <Buffer 00 00 00 00 ...>
console.log(bufA.length);
// 打印: 42
```

