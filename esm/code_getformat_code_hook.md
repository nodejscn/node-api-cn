
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

The `getFormat` hook provides a way to define a custom method of determining how
a URL should be interpreted. This can be one of the following:

| `format` | Description |
| --- | --- |
| `'builtin'` | Load a Node.js builtin module |
| `'commonjs'` | Load a Node.js CommonJS module |
| `'dynamic'` | Use a [dynamic instantiate hook][] |
| `'json'` | Load a JSON file |
| `'module'` | Load a standard JavaScript module (ES module) |
| `'wasm'` | Load a WebAssembly module |

```js
/**
 * @param {string} url
 * @param {object} context (currently empty)
 * @param {function} defaultGetFormat
 * @returns {object} response
 * @returns {string} response.format
 */
export async function getFormat(url, context, defaultGetFormat) {
  if (someCondition) {
    // For some or all URLs, do some custom logic for determining format.
    // Always return an object of the form {format: <string>}, where the
    // format is one of the strings in the table above.
    return {
      format: 'module'
    };
  }
  // Defer to Node.js for all other URLs.
  return defaultGetFormat(url, context, defaultGetFormat);
}
```

