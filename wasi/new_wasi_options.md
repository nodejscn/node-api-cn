<!-- YAML
added: v12.16.0
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

