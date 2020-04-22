
Currently importing JSON modules are only supported in the `commonjs` mode
and are loaded using the CJS loader. [WHATWG JSON modules specification][] are
still being standardized, and are experimentally supported by including the
additional flag `--experimental-json-modules` when running Node.js.

When the `--experimental-json-modules` flag is included both the
`commonjs` and `module` mode will use the new experimental JSON
loader. The imported JSON only exposes a `default`, there is no
support for named exports. A cache entry is created in the CommonJS
cache, to avoid duplication. The same object will be returned in
CommonJS if the JSON module has already been imported from the
same path.

Assuming an `index.mjs` with

<!-- eslint-skip -->
```js
import packageConfig from './package.json';
```

The `--experimental-json-modules` flag is needed for the module
to work.

```bash
node index.mjs # fails
node --experimental-json-modules index.mjs # works
```

