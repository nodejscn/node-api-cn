<!-- YAML
added: v5.10.0
-->

* `size` {integer} 新建的 `Buffer` 期望的长度
* `fill` {string|Buffer|integer} 用来预填充新建的 `Buffer` 的值。
  **默认:** `0`
* `encoding` {string} 如果 `fill` 是字符串，则该值是它的字符编码。
  **默认:** `'utf8'`

分配一个大小为 `size` 字节的新建的 `Buffer` 。
如果 `fill` 为 `undefined` ，则该 `Buffer` 会用 **0 填充**。

例子：

```js
const buf = Buffer.alloc(5);

// 输出: <Buffer 00 00 00 00 00>
console.log(buf);
```

分配一个大小为 `size` 字节的新建的 `Buffer` 。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`RangeError`] 错误。
如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

如果指定了 `fill` ，则会调用 [`buf.fill(fill)`] 初始化分配的 `Buffer` 。

例子：

```js
const buf = Buffer.alloc(5, 'a');

// 输出: <Buffer 61 61 61 61 61>
console.log(buf);
```

如果同时指定了 `fill` 和 `encoding` ，则会调用 [`buf.fill(fill, encoding)`] 初始化分配的 `Buffer` 。

例子：

```js
const buf = Buffer.alloc(11, 'aGVsbG8gd29ybGQ=', 'base64');

// 输出: <Buffer 68 65 6c 6c 6f 20 77 6f 72 6c 64>
console.log(buf);
```

调用 [`Buffer.alloc()`] 会明显地比另一个方法 [`Buffer.allocUnsafe()`] 慢，但是能确保新建的 `Buffer` 实例的内容**不会包含敏感数据**。

如果 `size` 不是一个数值，则抛出 `TypeError` 错误。

