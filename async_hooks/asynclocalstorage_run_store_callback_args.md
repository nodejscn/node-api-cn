<!-- YAML
added: v13.10.0
-->

* `store` {any}
* `callback` {Function}
* `...args` {any}

This methods runs a function synchronously within a context and return its
return value. The store is not accessible outside of the callback function or
the asynchronous operations created within the callback.

Optionally, arguments can be passed to the function. They will be passed to
the callback function.

If the callback function throws an error, it will be thrown by `run` too.
The stacktrace will not be impacted by this call and the context will
be exited.

Example:

```js
const store = { id: 2 };
try {
  asyncLocalStorage.run(store, () => {
    asyncLocalStorage.getStore(); // Returns the store object
    throw new Error();
  });
} catch (e) {
  asyncLocalStorage.getStore(); // Returns undefined
  // The error will be caught here
}
```

