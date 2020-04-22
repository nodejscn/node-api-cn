<!-- YAML
added: v11.12.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer considered experimental.
-->

* {string}

Filename where the report is written. If set to the empty string, the output
filename will be comprised of a timestamp, PID, and sequence number. The default
value is the empty string.

```js
console.log(`Report filename is ${process.report.filename}`);
```

