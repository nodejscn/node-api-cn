<!-- YAML
added: v0.1.90
-->

* {integer}

返回 `buf` 在字节数上分配的内存量。
注意，这并不一定反映 `buf` 内可用的数据量。

例子：创建一个 `Buffer` 并写入一个较短的 ASCII 字符串。

```js
const buf = Buffer.alloc(1234);

// 输出: 1234
console.log(buf.length);

buf.write('some string', 0, 'ascii');

// 输出: 1234
console.log(buf.length);
```

虽然 `length` 属性不是不可变的，但改变 `length` 的值可能会导致不确定、不一致的行为。
那些希望修改一个 `Buffer` 的长度的应用程序应当将 `length` 视为只读的，且使用 [`buf.slice()`] 创建一个新的 `Buffer`。

例子：

```js
let buf = Buffer.allocUnsafe(10);

buf.write('abcdefghj', 0, 'ascii');

// 输出: 10
console.log(buf.length);

buf = buf.slice(0, 5);

// 输出: 5
console.log(buf.length);
```

