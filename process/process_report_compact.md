<!-- YAML
added: v13.12.0
-->

* {boolean}

Write reports in a compact format, single-line JSON, more easily consumable
by log processing systems than the default multi-line format designed for
human consumption.

```js
console.log(`Reports are compact? ${process.report.compact}`);
```

