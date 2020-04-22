<!-- YAML
added: v11.12.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer considered experimental.
-->

* {string}

Directory where the report is written. The default value is the empty string,
indicating that reports are written to the current working directory of the
Node.js process.

```js
console.log(`Report directory is ${process.report.directory}`);
```

