
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

The `resolve` hook returns the resolved file URL for a given module specifier
and parent URL. The module specifier is the string in an `import` statement or
`import()` expression, and the parent URL is the URL of the module that imported
this one, or `undefined` if this is the main entry point for the application.

```js
/**
 * @param {string} specifier
 * @param {object} context
 * @param {string} context.parentURL
 * @param {function} defaultResolve
 * @returns {object} response
 * @returns {string} response.url
 */
export async function resolve(specifier, context, defaultResolve) {
  const { parentURL = null } = context;
  if (someCondition) {
    // For some or all specifiers, do some custom logic for resolving.
    // Always return an object of the form {url: <string>}
    return {
      url: (parentURL) ?
        new URL(specifier, parentURL).href : new URL(specifier).href
    };
  }
  // Defer to Node.js for all other specifiers.
  return defaultResolve(specifier, context, defaultResolve);
}
```

