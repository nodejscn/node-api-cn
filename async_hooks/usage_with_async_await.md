
If, within an async function, only one `await` call is to run within a context,
the following pattern should be used:

```js
async function fn() {
  await asyncLocalStorage.run(new Map(), () => {
    asyncLocalStorage.getStore().set('key', value);
    return foo(); // The return value of foo will be awaited
  });
}
```

In this example, the store is only available in the callback function and the
functions called by `foo`. Outside of `run`, calling `getStore` will return
`undefined`.

