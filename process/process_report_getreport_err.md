<!-- YAML
added: v11.8.0
-->

> Stability: 1 - Experimental

* `err` {Error} A custom error used for reporting the JavaScript stack.
* Returns: {Object}

Returns a JavaScript Object representation of a diagnostic report for the
running process. The report's JavaScript stack trace is taken from `err`, if
present.

```js
const data = process.report.getReport();
console.log(data.header.nodeJsVersion);

// Similar to process.report.writeReport()
const fs = require('fs');
fs.writeFileSync(util.inspect(data), 'my-report.log', 'utf8');
```

Additional documentation is available in the [report documentation][].

