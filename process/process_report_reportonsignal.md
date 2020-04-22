<!-- YAML
added: v11.12.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer considered experimental.
-->

* {boolean}

If `true`, a diagnostic report is generated when the process receives the
signal specified by `process.report.signal`.

```js
console.log(`Report on signal: ${process.report.reportOnSignal}`);
```

