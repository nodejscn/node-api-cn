<!-- YAML
added: v11.12.0
-->

> Stability: 1 - Experimental

* {string}

The signal used to trigger the creation of a diagnostic report. Defaults to
`'SIGUSR2'`.

```js
console.log(`Report signal: ${process.report.signal}`);
```

