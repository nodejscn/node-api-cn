
JSON modules follow the [WHATWG JSON modules specification][].

The imported JSON only exposes a `default`. There is no
support for named exports. A cache entry is created in the CommonJS
cache, to avoid duplication. The same object will be returned in
CommonJS if the JSON module has already been imported from the
same path.

Assuming an `index.mjs` with

<!-- eslint-skip -->
```js
import packageConfig from './package.json';
```

