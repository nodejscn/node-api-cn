<!-- YAML
added:
 - v13.10.0
 - v12.17.0
-->

* `callback` {Function}
* `...args` {any}

Runs a function synchronously outside of a context and returns its
return value. The store is not accessible within the callback function or
the asynchronous operations created within the callback. Any `getStore()`
call done within the callback function will always return `undefined`.

The optional `args` are passed to the callback function.

If the callback function throws an error, the error is thrown by `exit()` too.
The stacktrace is not impacted by this call and the context is re-entered.

Example:

```js
// Within a call to run
try {
  asyncLocalStorage.getStore(); // Returns the store object or value
  asyncLocalStorage.exit(() => {
    asyncLocalStorage.getStore(); // Returns undefined
    throw new Error();
  });
} catch (e) {
  asyncLocalStorage.getStore(); // Returns the same object or value
  // The error will be caught here
}
```

