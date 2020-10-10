<!-- YAML
added: v11.12.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer experimental.
-->

* {string}

The signal used to trigger the creation of a diagnostic report. Defaults to
`'SIGUSR2'`.

```js
console.log(`Report signal: ${process.report.signal}`);
```

