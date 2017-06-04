<!-- YAML
added: v0.3.1
changes:
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4777
    description: The `cachedData` and `produceCachedData` options are
                 supported now.
-->

* `code` {string} The JavaScript code to compile.
* `options`
  * `filename` {string} Specifies the filename used in stack traces produced
    by this script.
  * `lineOffset` {number} Specifies the line number offset that is displayed
    in stack traces produced by this script.
  * `columnOffset` {number} Specifies the column number offset that is displayed
    in stack traces produced by this script.
  * `displayErrors` {boolean} When `true`, if an [`Error`][] error occurs
    while compiling the `code`, the line of code causing the error is attached
    to the stack trace.
  * `timeout` {number} Specifies the number of milliseconds to execute `code`
    before terminating execution. If execution is terminated, an [`Error`][]
    will be thrown.
  * `cachedData` {Buffer} Provides an optional `Buffer` with V8's code cache
    data for the supplied source. When supplied, the `cachedDataRejected` value
    will be set to either `true` or `false` depending on acceptance of the data
    by V8.
  * `produceCachedData` {boolean} When `true` and no `cachedData` is present, V8
    will attempt to produce code cache data for `code`. Upon success, a
    `Buffer` with V8's code cache data will be produced and stored in the
    `cachedData` property of the returned `vm.Script` instance.
    The `cachedDataProduced` value will be set to either `true` or `false`
    depending on whether code cache data is produced successfully.

Creating a new `vm.Script` object compiles `code` but does not run it. The
compiled `vm.Script` can be run later multiple times. It is important to note
that the `code` is not bound to any global object; rather, it is bound before
each run, just for that run.

