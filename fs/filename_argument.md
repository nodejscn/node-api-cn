
<!--type=misc-->

Providing `filename` argument in the callback is only supported on Linux and
Windows.  Even on supported platforms, `filename` is not always guaranteed to
be provided. Therefore, don't assume that `filename` argument is always
provided in the callback, and have some fallback logic if it is null.

```js
fs.watch('somedir', (eventType, filename) => {
  console.log(`event type is: ${eventType}`);
  if (filename) {
    console.log(`filename provided: ${filename}`);
  } else {
    console.log('filename not provided');
  }
});
```

