<!-- YAML
added:
 - v13.3.0
 - v12.16.0
-->

* `options` {Object}
  * `args` {Array} An array of strings that the WebAssembly application will
    see as command line arguments. The first argument is the virtual path to the
    WASI command itself. **Default:** `[]`.
  * `env` {Object} An object similar to `process.env` that the WebAssembly
    application will see as its environment. **Default:** `{}`.
  * `preopens` {Object} This object represents the WebAssembly application's
    sandbox directory structure. The string keys of `preopens` are treated as
    directories within the sandbox. The corresponding values in `preopens` are
    the real paths to those directories on the host machine.
  * `returnOnExit` {boolean} By default, WASI applications terminate the Node.js
    process via the `__wasi_proc_exit()` function. Setting this option to `true`
    causes `wasi.start()` to return the exit code rather than terminate the
    process. **Default:** `false`.
  * `stdin` {integer} The file descriptor used as standard input in the
    WebAssembly application. **Default:** `0`.
  * `stdout` {integer} The file descriptor used as standard output in the
    WebAssembly application. **Default:** `1`.
  * `stderr` {integer} The file descriptor used as standard error in the
    WebAssembly application. **Default:** `2`.

