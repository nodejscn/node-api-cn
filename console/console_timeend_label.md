<!-- YAML
added: v0.1.104
-->

Stops a timer that was previously started by calling [`console.time()`][] and
prints the result to `stdout`:

```js
console.time('100-elements');
for (var i = 0; i < 100; i++) {
  ;
}
console.timeEnd('100-elements');
// prints 100-elements: 225.438ms
```

*Note: As of Node.js v6.0.0, `console.timeEnd()` deletes the timer to avoid
leaking it. On older versions, the timer persisted. This allowed
`console.timeEnd()` to be called multiple times for the same label. This
functionality was unintended and is no longer supported.*

