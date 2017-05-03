<!-- YAML
added: v5.10.0
-->

* `array` {Array}

通过一个八位字节的 `array` 创建一个新的 `Buffer` 。

例子：

```js
// 创建一个新的包含字符串 'buffer' 的 UTF-8 字节的 Buffer
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```

如果 `array` 不是一个数组，则抛出 `TypeError` 错误。

