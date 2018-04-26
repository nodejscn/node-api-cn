<!-- YAML
added: v0.5.0
-->

* {string}

`process.arch`属性返回一个表示操作系统CPU架构的字符串，Node.js二进制文件是为这些架构编译的。
例如
`'arm'`, `'arm64'`, `'ia32'`, `'mips'`, `'mipsel'`, `'ppc'`, `'ppc64'`, `'s390'`, `'s390x'`, `'x32'`, 或 `'x64'`。

```js
console.log(`This processor architecture is ${process.arch}`);
```

