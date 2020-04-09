
> Note: The loaders API is being redesigned. This hook may disappear or its
> signature may change. Do not rely on the API described below.

Sometimes it can be necessary to run some code inside of the same global scope
that the application will run in. This hook allows to return a string that will
be ran as sloppy-mode script on startup.

Similar to how CommonJS wrappers work, the code runs in an implicit function
scope. The only argument is a `require`-like function that can be used to load
builtins like "fs": `getBuiltin(request: string)`.

If the code needs more advanced `require` features, it will have to construct
its own `require` using  `module.createRequire()`.

```js
/**
 * @returns {string} Code to run before application startup
 */
export function getGlobalPreloadCode() {
  return `\
globalThis.someInjectedProperty = 42;
console.log('I just set some globals!');

const { createRequire } = getBuiltin('module');

const require = createRequire(process.cwd + '/<preload>');
// [...]
`;
}
```

