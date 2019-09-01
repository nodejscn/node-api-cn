<!-- YAML
added: v11.12.0
-->

> Stability: 1 - Experimental

* {string}

Filename where the report is written. If set to the empty string, the output
filename will be comprised of a timestamp, PID, and sequence number. The default
value is the empty string.

```js
console.log(`Report filename is ${process.report.filename}`);
```

