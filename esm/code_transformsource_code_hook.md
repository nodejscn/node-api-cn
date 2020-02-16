
```console
NODE_OPTIONS='--experimental-modules --experimental-loader ./custom-loader.mjs' node x.js
```

> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

The `transformSource` hook provides a way to modify the source code of a loaded
ES module file after the source string has been loaded but before Node.js has
done anything with it.

If this hook is used to convert unknown-to-Node.js file types into executable
JavaScript, a resolve hook is also necessary in order to register any
unknown-to-Node.js file extensions. See the [transpiler loader example][] below.

```js
/**
 * @param {string|buffer} source
 * @param {object} context
 * @param {string} context.url
 * @param {string} context.format
 * @param {function} defaultTransformSource
 * @returns {object} response
 * @returns {string|buffer} response.source
 */
export async function transformSource(source,
                                      context,
                                      defaultTransformSource) {
  const { url, format } = context;
  if (someCondition) {
    // For some or all URLs, do some custom logic for modifying the source.
    // Always return an object of the form {source: <string|buffer>}.
    return {
      source: '...'
    };
  }
  // Defer to Node.js for all other sources.
  return defaultTransformSource(
    source, context, defaultTransformSource);
}
```

