<!-- YAML
added: v11.12.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer experimental.
-->

* {boolean}

If `true`, a diagnostic report is generated on uncaught exception.

```js
console.log(`Report on exception: ${process.report.reportOnUncaughtException}`);
```

