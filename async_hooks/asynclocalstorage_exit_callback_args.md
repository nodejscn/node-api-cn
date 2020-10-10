<!-- YAML
added: v13.10.0
-->

* `callback` {Function}
* `...args` {any}

This methods runs a function synchronously outside of a context and return its
return value. The store is not accessible within the callback function or
the asynchronous operations created within the callback.

Optionally, arguments can be passed to the function. They will be passed to
the callback function.

If the callback function throws an error, it will be thrown by `exit` too.
The stacktrace will not be impacted by this call and
the context will be re-entered.

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

