
> Stability: 1 - Experimental

Importing Web Assembly modules is supported under the
`--experimental-wasm-modules` flag, allowing any `.wasm` files to be
imported as normal modules while also supporting their module imports.

This integration is in line with the
[ES Module Integration Proposal for Web Assembly][].

For example, an `index.mjs` containing:

```js
import * as M from './module.wasm';
console.log(M);
```

executed under:

```bash
node --experimental-wasm-modules index.mjs
```

would provide the exports interface for the instantiation of `module.wasm`.

<i id="esm_experimental_top_level_await"></i>

