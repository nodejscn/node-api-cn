
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

* `url` {string}
* `context` {Object}
* `defaultGetFormat` {Function}
* Returns: {Object}
  * `format` {string}

The `getFormat` hook provides a way to define a custom method of determining how
a URL should be interpreted. The `format` returned also affects what the
acceptable forms of source values are for a module when parsing. This can be one
of the following:

| `format`     | Description                    | Acceptable Types For `source` Returned by `getSource` or `transformSource` |
| ------------ | ------------------------------ | -------------------------------------------------------------------------- |
| `'builtin'`  | Load a Node.js builtin module  | Not applicable                                                             |
| `'commonjs'` | Load a Node.js CommonJS module | Not applicable                                                             |
| `'json'`     | Load a JSON file               | { [`string`][], [`ArrayBuffer`][], [`TypedArray`][] }                      |
| `'module'`   | Load an ES module              | { [`string`][], [`ArrayBuffer`][], [`TypedArray`][] }                      |
| `'wasm'`     | Load a WebAssembly module      | { [`ArrayBuffer`][], [`TypedArray`][] }                                    |

Note: These types all correspond to classes defined in ECMAScript.

* The specific [`ArrayBuffer`][] object is a [`SharedArrayBuffer`][].
* The specific [`TypedArray`][] object is a [`Uint8Array`][].

Note: If the source value of a text-based format (i.e., `'json'`, `'module'`) is
not a string, it will be converted to a string using [`util.TextDecoder`][].

```js
/**
 * @param {string} url
 * @param {Object} context (currently empty)
 * @param {Function} defaultGetFormat
 * @returns {Promise<{ format: string }>}
 */
export async function getFormat(url, context, defaultGetFormat) {
  if (Math.random() > 0.5) { // Some condition.
    // For some or all URLs, do some custom logic for determining format.
    // Always return an object of the form {format: <string>}, where the
    // format is one of the strings in the table above.
    return {
      format: 'module',
    };
  }
  // Defer to Node.js for all other URLs.
  return defaultGetFormat(url, context, defaultGetFormat);
}
```

