<!-- YAML
added: v0.5.0
-->

* {string}

The `process.arch` property returns a String identifying the processor
architecture that the Node.js process is currently running on. For instance
`'arm'`, `'ia32'`, or `'x64'`.

```js
console.log(`This processor architecture is ${process.arch}`);
```

