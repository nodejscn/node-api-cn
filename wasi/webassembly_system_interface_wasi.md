
<!--introduced_in=v12.16.0-->

> Stability: 1 - Experimental

<!-- source_link=lib/wasi.js -->

The WASI API provides an implementation of the [WebAssembly System Interface][]
specification. WASI gives sandboxed WebAssembly applications access to the
underlying operating system via a collection of POSIX-like functions.

```mjs
import fs from 'fs';
import { WASI } from 'wasi';

const wasi = new WASI({
  args: process.argv,
  env: process.env,
  preopens: {
    '/sandbox': '/some/real/path/that/wasm/can/access'
  }
});
const importObject = { wasi_snapshot_preview1: wasi.wasiImport };

const wasm = await WebAssembly.compile(fs.readFileSync('./demo.wasm'));
const instance = await WebAssembly.instantiate(wasm, importObject);

wasi.start(instance);
```

```cjs
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
  const wasm = await WebAssembly.compile(fs.readFileSync('./demo.wasm'));
  const instance = await WebAssembly.instantiate(wasm, importObject);

  wasi.start(instance);
})();
```

To run the above example, create a new WebAssembly text format file named
`demo.wat`:

```text
(module
    ;; Import the required fd_write WASI function which will write the given io vectors to stdout
    ;; The function signature for fd_write is:
    ;; (File Descriptor, *iovs, iovs_len, nwritten) -> Returns number of bytes written
    (import "wasi_snapshot_preview1" "fd_write" (func $fd_write (param i32 i32 i32 i32) (result i32)))

    (memory 1)
    (export "memory" (memory 0))

    ;; Write 'hello world\n' to memory at an offset of 8 bytes
    ;; Note the trailing newline which is required for the text to appear
    (data (i32.const 8) "hello world\n")

    (func $main (export "_start")
        ;; Creating a new io vector within linear memory
        (i32.store (i32.const 0) (i32.const 8))  ;; iov.iov_base - This is a pointer to the start of the 'hello world\n' string
        (i32.store (i32.const 4) (i32.const 12))  ;; iov.iov_len - The length of the 'hello world\n' string

        (call $fd_write
            (i32.const 1) ;; file_descriptor - 1 for stdout
            (i32.const 0) ;; *iovs - The pointer to the iov array, which is stored at memory location 0
            (i32.const 1) ;; iovs_len - We're printing 1 string stored in an iov - so one.
            (i32.const 20) ;; nwritten - A place in memory to store the number of bytes written
        )
        drop ;; Discard the number of bytes written from the top of the stack
    )
)
```

Use [wabt](https://github.com/WebAssembly/wabt) to compile `.wat` to `.wasm`

```console
$ wat2wasm demo.wat
```

The `--experimental-wasi-unstable-preview1` CLI argument is needed for this
example to run.

