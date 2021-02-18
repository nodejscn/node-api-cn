<!-- YAML
added: v0.1.3
-->

* {string}

`process.version` 属性包含 Node.js 版本的字符串。

```js
console.log(`版本: ${process.version}`);
// 版本: v14.8.0
```

若要获取不带前缀 _v_ 的版本字符串，则使用 `process.versions.node`。

