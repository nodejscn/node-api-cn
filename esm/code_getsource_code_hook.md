
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

The `getSource` hook provides a way to define a custom method for retrieving
the source code of an ES module specifier. This would allow a loader to
potentially avoid reading files from disk.

```js
/**
 * @param {string} url
 * @param {{ format: string }} context
 * @param {Function} defaultGetSource
 * @returns {Promise<{ source: !(SharedArrayBuffer | string | Uint8Array) }>}
 */
export async function getSource(url, context, defaultGetSource) {
  const { format } = context;
  if (Math.random() > 0.5) { // Some condition.
    // For some or all URLs, do some custom logic for retrieving the source.
    // Always return an object of the form {source: <string|buffer>}.
    return {
      source: '...',
    };
  }
  // Defer to Node.js for all other URLs.
  return defaultGetSource(url, context, defaultGetSource);
}
```

