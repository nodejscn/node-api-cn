<!-- YAML
added: v0.1.90
-->

* {integer}

返回 `buf` 中的字节数。

```js
// 创建一个 `Buffer`，并使用 UTF-8 写入一个短的字符串。

const buf = Buffer.alloc(1234);

console.log(buf.length);
// 打印: 1234

buf.write('http://nodejs.cn/', 0, 'utf8');

console.log(buf.length);
// 打印: 1234
```
