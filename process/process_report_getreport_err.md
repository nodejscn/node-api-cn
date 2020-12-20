<!-- YAML
added: v11.8.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer experimental.
-->

* `err` {Error} A custom error used for reporting the JavaScript stack.
* Returns: {Object}

Returns a JavaScript Object representation of a diagnostic report for the
running process. The report's JavaScript stack trace is taken from `err`, if
present.

```js
const data = process.report.getReport();
console.log(data.header.nodejsVersion);

// Similar to process.report.writeReport()
const fs = require('fs');
fs.writeFileSync(util.inspect(data), 'my-report.log', 'utf8');
```

Additional documentation is available in the [report documentation][].

