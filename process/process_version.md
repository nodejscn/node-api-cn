<!-- YAML
added: v0.1.3
-->

* {string}

`process.version` 属性包含 Node.js 的版本字符串。

```js
console.log(`版本: ${process.version}`);
// 版本: v14.8.0
```

To get the version string without the prepended _v_, use
`process.versions.node`.

