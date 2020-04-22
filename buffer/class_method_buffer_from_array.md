<!-- YAML
added: v5.10.0
-->

* `array` {integer[]}

使用 `0` – `255` 范围内的字节数组 `array` 来分配一个新的 `Buffer`。
超出该范围的数组条目会被截断以适合它。

```js
// 创建一个包含字符串 'buffer' 的 UTF-8 字节的新 Buffer。
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```

如果 `array` 不是一个 `Array` 或适用于 `Buffer.from()` 变量的其他类型，则抛出 `TypeError`。

`Buffer.from(array)` 和 [`Buffer.from(string)`] 也可以像 [`Buffer.allocUnsafe()`] 一样使用内部的 `Buffer` 池。

