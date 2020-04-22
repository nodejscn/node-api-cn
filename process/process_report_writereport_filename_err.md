<!-- YAML
added: v11.8.0
changes:
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This API is no longer considered experimental.
-->

* `filename` {string} Name of the file where the report is written. This
  should be a relative path, that will be appended to the directory specified in
  `process.report.directory`, or the current working directory of the Node.js
  process, if unspecified.
* `err` {Error} A custom error used for reporting the JavaScript stack.

* Returns: {string} Returns the filename of the generated report.

Writes a diagnostic report to a file. If `filename` is not provided, the default
filename includes the date, time, PID, and a sequence number. The report's
JavaScript stack trace is taken from `err`, if present.

```js
process.report.writeReport();
```

Additional documentation is available in the [report documentation][].

