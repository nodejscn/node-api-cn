
Relative resolution can be handled via `new URL('./local', import.meta.url)`.

For a complete `require.resolve` replacement, there is a flagged experimental
[`import.meta.resolve`][] API.

Alternatively `module.createRequire()` can be used.

