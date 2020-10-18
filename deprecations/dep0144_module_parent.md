<!-- YAML
changes:
  - version:
    - v14.6.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/32217
    description: Documentation-only deprecation.
-->

Type: Documentation-only

A CommonJS module can access the first module that required it using
`module.parent`. This feature is deprecated because it does not work
consistently in the presence of ECMAScript modules and because it gives an
inaccurate representation of the CommonJS module graph.

Some modules use it to check if they are the entry point of the current process.
Instead, it is recommended to compare `require.main` and `module`:

```js
if (require.main === module) {
  // Code section that will run only if current file is the entry point.
}
```

When looking for the CommonJS modules that have required the current one,
`require.cache` and `module.children` can be used:

```js
const moduleParents = Object.values(require.cache)
  .filter((m) => m.children.includes(module));
```

