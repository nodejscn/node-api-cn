<!-- YAML
added: v11.12.0
changes:
  - version:
     - v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35654
    description: This API is no longer experimental.
-->

* {boolean}

If `true`, a diagnostic report is generated on fatal errors, such as out of
memory errors or failed C++ assertions.

```js
console.log(`Report on fatal error: ${process.report.reportOnFatalError}`);
```

