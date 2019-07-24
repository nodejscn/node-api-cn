
Files ending with `.js` or `.mjs`, or lacking any extension,
will be loaded as ES modules when the nearest parent `package.json` file
contains a top-level field `"type"` with a value of `"module"`.

The nearest parent `package.json` is defined as the first `package.json` found
when searching in the current folder, that folder’s parent, and so on up
until the root of the volume is reached.

<!-- eslint-skip -->
```js
// package.json
{
  "type": "module"
}
```

```sh
