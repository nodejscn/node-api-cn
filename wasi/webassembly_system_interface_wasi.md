
<!--introduced_in=v12.16.0-->

> Stability: 1 - Experimental

The WASI API provides an implementation of the [WebAssembly System Interface][]
specification. WASI gives sandboxed WebAssembly applications access to the
underlying operating system via a collection of POSIX-like functions.

```js
'use strict';
const fs = require('fs');
const { WASI } = require('wasi');
const wasi = new WASI({
  args: process.argv,
  env: process.env,
  preopens: {
    '/sandbox': '/some/real/path/that/wasm/can/access'
  }
});
const importObject = { wasi_snapshot_preview1: wasi.wasiImport };

(async () => {
  const wasm = await WebAssembly.compile(fs.readFileSync('./binary.wasm'));
  const instance = await WebAssembly.instantiate(wasm, importObject);

  wasi.start(instance);
})();
```

The `--experimental-wasi-unstable-preview1` and `--experimental-wasm-bigint`
CLI arguments are needed for the previous example to run.

