<!-- YAML
added: v0.9.1
-->

* `encoding` {string} 要检查的字符编码名称。
* 返回: {boolean}

如果 `encoding` 是支持的字符编码的名称，则返回 `true`，否则返回 `false`。

```js
console.log(Buffer.isEncoding('utf-8'));
// 打印: true

console.log(Buffer.isEncoding('hex'));
// 打印: true

console.log(Buffer.isEncoding('utf/8'));
// 打印: false

console.log(Buffer.isEncoding(''));
// 打印: false
```

