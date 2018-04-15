<!-- YAML
added: v0.5.0
-->

* {string}

The `process.arch` property returns a string identifying the operating system CPU
architecture for which the Node.js binary was compiled.

例如
`'arm'`, `'arm64'`, `'ia32'`, `'mips'`, `'mipsel'`, `'ppc'`, `'ppc64'`, `'s390'`, `'s390x'`, `'x32'`, 或 `'x64'`。

```js
console.log(`This processor architecture is ${process.arch}`);
```

