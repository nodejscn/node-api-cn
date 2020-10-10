<!-- YAML
added: v11.12.0
-->

> Stability: 1 - Experimental

* {boolean}

If `true`, a diagnostic report is generated on fatal errors, such as out of
memory errors or failed C++ assertions.

```js
console.log(`Report on fatal error: ${process.report.reportOnFatalError}`);
```

