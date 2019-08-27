
```js
(async function() {
  for await (const chunk of readable) {
    console.log(chunk);
  }
})();
```

Async iterators register a permanent error handler on the stream to prevent any
unhandled post-destroy errors.

