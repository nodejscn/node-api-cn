<!-- YAML
added: v5.10.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18129
    description: Attempting to fill a non-zero length buffer with a zero length
                 buffer triggers a thrown exception.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17427
    description: Specifying an invalid string for `fill` triggers a thrown
                 exception.
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/17428
    description: Specifying an invalid string for `fill` now results in a
                 zero-filled buffer.
-->

* `size` {integer} 新建的 `Buffer` 的长度。
* `fill` {string|Buffer|integer} 预填充 `Buffer` 的值。默认为 `0`。
* `encoding` {string} 如果 `fill` 是字符串，则指定 `fill` 的字符编码。默认为 `'utf8'`。

创建一个大小为 `size` 字节的 `Buffer`。
如果 `fill` 为 `undefined`，则用 0 填充 `Buffer`。

```js
const buf = Buffer.alloc(5);

console.log(buf);
// 输出: <Buffer 00 00 00 00 00>
```

如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`ERR_INVALID_OPT_VALUE`]。
如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

如果指定了 `fill`，则调用 [`buf.fill(fill)`][`buf.fill()`] 初始化 `Buffer`。

```js
const buf = Buffer.alloc(5, 'a');

console.log(buf);
// 输出: <Buffer 61 61 61 61 61>

```

如果同时指定了 `fill` 和 `encoding`，则调用 [`buf.fill(fill, encoding)`][`buf.fill()`] 初始化 `Buffer`。

```js
const buf = Buffer.alloc(11, 'aGVsbG8gd29ybGQ=', 'base64');

console.log(buf);
// 输出: <Buffer 68 65 6c 6c 6f 20 77 6f 72 6c 64>
```

`Buffer.alloc()` 比 [`Buffer.allocUnsafe()`] 慢，但能确保新建的 `Buffer` 不会包含旧数据。

