
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

The `resolve` hook returns the resolved file URL for a given module specifier
and parent URL. The module specifier is the string in an `import` statement or
`import()` expression, and the parent URL is the URL of the module that imported
this one, or `undefined` if this is the main entry point for the application.

The `conditions` property on the `context` is an array of conditions for
[Conditional Exports][] that apply to this resolution request. They can be used
for looking up conditional mappings elsewhere or to modify the list when calling
the default resolution logic.

The [current set of Node.js default conditions][Conditional Exports] will always
be in the `context.conditions` list passed to the hook. If the hook wants to
ensure Node.js-compatible resolution logic, all items from this default
condition list **must** be passed through to the `defaultResolve` function.

```js
/**
 * @param {string} specifier
 * @param {object} context
 * @param {string} context.parentURL
 * @param {string[]} context.conditions
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
  if (anotherCondition) {
    // When calling the defaultResolve, the arguments can be modified. In this
    // case it's adding another value for matching conditional exports.
    return defaultResolve(specifier, {
      ...context,
      conditions: [...context.conditions, 'another-condition'],
    });
  }
  // Defer to Node.js for all other specifiers.
  return defaultResolve(specifier, context, defaultResolve);
}
```

