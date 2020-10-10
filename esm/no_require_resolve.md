
Former use cases relying on `require.resolve` to determine the resolved path
of a module can be supported via `import.meta.resolve`, which is experimental
and supported via the `--experimental-import-meta-resolve` flag:

```js
(async () => {
  const dependencyAsset = await import.meta.resolve('component-lib/asset.css');
})();
```

`import.meta.resolve` also accepts a second argument which is the parent module
from which to resolve from:

```js
(async () => {
  // Equivalent to import.meta.resolve('./dep')
  await import.meta.resolve('./dep', import.meta.url);
})();
```

This function is asynchronous because the ES module resolver in Node.js is
asynchronous. With the introduction of [Top-Level Await][], these use cases
will be easier as they won't require an async function wrapper.

