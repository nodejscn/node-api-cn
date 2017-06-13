<!-- YAML
added: v0.5.0
-->

* {string}

`process.arch`属性返回一个标识Node.js在其上运行的处理器架构的字符串。例如
`'arm'`, `'ia32'`, or `'x64'`.

```js
console.log(`This processor architecture is ${process.arch}`);
```

