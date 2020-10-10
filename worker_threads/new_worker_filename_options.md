<!-- YAML
added: v10.5.0
changes:
  - version: v14.9.0
    pr-url: https://github.com/nodejs/node/pull/34584
    description: The `filename` parameter can be a WHATWG `URL` object using
                 `data:` protocol.
  - version: v14.9.0
    pr-url: https://github.com/nodejs/node/pull/34394
    description: The `trackUnmanagedFds` option was set to `true` by default.
  - version:
    - v14.6.0
    pr-url: https://github.com/nodejs/node/pull/34303
    description: The `trackUnmanagedFds` option was introduced.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/32278
    description: The `transferList` option was introduced.
  - version: v13.12.0
    pr-url: https://github.com/nodejs/node/pull/31664
    description: The `filename` parameter can be a WHATWG `URL` object using
                 `file:` protocol.
  - version:
     - v13.2.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/26628
    description: The `resourceLimits` option was introduced.
  - version:
     - v13.4.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30559
    description: The `argv` option was introduced.
-->

* `filename` {string} 工作线程主脚本的路径。必须是以 `./` 或 `../` 开头的绝对路径或相对路径（即相对于当前工作目录）、或者使用 `file:` 或 `data:` 协议的 WHATWG `URL` 对象。 
   When using a [`data:` URL][], the data is interpreted based on MIME type using the [ECMAScript module loader][].
   如果 `options.eval` 为 `true`，则这是一个包含 JavaScript 代码而不是路径的字符串。
* `options` {Object}
  * `argv` {any[]} 参数列表，其将会被字符串化并附加到工作线程中的 `process.argv`。
    这大部分与 `workerData` 相似，但是这些值将会在全局的 `process.argv` 中可用，就好像它们是作为 CLI 选项传给脚本一样。
  * `env` {Object} 如果设置，则指定工作线程中 `process.env` 的初始值。
     作为一个特殊值，[`worker.SHARE_ENV`] 可以用于指定父线程和子线程应该共享它们的环境变量。
     在这种情况下，对一个线程的 `process.env` 对象的更改也会影响另一个线程。
     **默认值:** `process.env`。
  * `eval` {boolean} 如果为 `true` 且第一个参数是一个 `string`，则将构造函数的第一个参数解释为工作线程联机后执行的脚本。
  * `execArgv` {string[]} 传递给工作线程的 node CLI 选项的列表。
     不支持 V8 选项（例如 `--max-old-space-size`）和影响进程的选项（例如 `--title`）。
     如果设置，则它将会作为工作线程内部的 [`process.execArgv`] 提供。
     默认情况下，选项将会从父线程继承。
  * `stdin` {boolean} 如果将其设置为 `true`，则 `worker.stdin` 将会提供一个可写流，其内容将会在工作线程中以 `process.stdin` 出现。
     默认情况下，不提供任何数据。
  * `stdout` {boolean} 如果将其设置为 `true`，则 `worker.stdout` 将不会自动地通过管道传递到父线程中的 `process.stdout`。
  * `stderr` {boolean} 如果将其设置为 `true`，则 `worker.stderr` 将不会自动地通过管道传递到父线程中的 `process.stderr`。
  * `workerData` {any} 能被克隆并作为 [`require('worker_threads').workerData`] 的任何 JavaScript 值。
     克隆将会按照 [HTML 结构化克隆算法][HTML structured clone algorithm]中描述的进行，如果对象无法被克隆（例如，因为它包含 `function`），则会抛出错误。
  * `trackUnmanagedFds` {boolean} If this is set to `true`, then the Worker will
    track raw file descriptors managed through [`fs.open()`][] and
    [`fs.close()`][], and close them when the Worker exits, similar to other
    resources like network sockets or file descriptors managed through
    the [`FileHandle`][] API. This option is automatically inherited by all
    nested `Worker`s. **Default**: `false`.
  * `transferList` {Object[]} If one or more `MessagePort`-like objects
    are passed in `workerData`, a `transferList` is required for those
    items or [`ERR_MISSING_MESSAGE_PORT_IN_TRANSFER_LIST`][] will be thrown.
    See [`port.postMessage()`][] for more information.
  * `resourceLimits` {Object} 新的 JS 引擎实例的一组可选的资源限制。 
    达到这些限制将会导致终止 `Worker` 实例。 
    这些限制仅影响 JS 引擎，并且不影响任何外部数据，包括 `ArrayBuffers`。 
    即使设置了这些限制，如果遇到全局内存不足的情况，该进程仍可能中止。
    * `maxOldGenerationSizeMb` {number} 主堆的最大大小，以 MB 为单位。
    * `maxYoungGenerationSizeMb` {number} 最近创建的对象的堆空间的最大大小。
    * `codeRangeSizeMb` {number} 用于生成代码的预分配的内存范围的大小。
    * `stackSizeMb` {number} The default maximum stack size for the thread.
      Small values may lead to unusable Worker instances. **Default:** `4`.

