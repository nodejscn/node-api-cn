<!-- YAML
added:
 - v13.10.0
 - v12.17.0
-->

* `store` {any}
* `callback` {Function}
* `...args` {any}

Runs a function synchronously within a context and returns its
return value. The store is not accessible outside of the callback function.
The store is accessible to any asynchronous operations created within the
callback.

The optional `args` are passed to the callback function.

If the callback function throws an error, the error is thrown by `run()` too.
The stacktrace is not impacted by this call and the context is exited.

Example:

```js
const store = { id: 2 };
try {
  asyncLocalStorage.run(store, () => {
    asyncLocalStorage.getStore(); // Returns the store object
    setTimeout(() => {
      asyncLocalStorage.getStore(); // Returns the store object
    }, 200);
    throw new Error();
  });
} catch (e) {
  asyncLocalStorage.getStore(); // Returns undefined
  // The error will be caught here
}
```

