<!-- YAML
added: v11.12.0
-->

> Stability: 1 - Experimental

* {string}

Directory where the report is written. The default value is the empty string,
indicating that reports are written to the current working directory of the
Node.js process.

```js
console.log(`Report directory is ${process.report.directory}`);
```

