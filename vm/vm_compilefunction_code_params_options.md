<!-- YAML
added: v10.10.0
-->
* `code` {string} The body of the function to compile.
* `params` {string[]} An array of strings containing all parameters for the
  function.
* `options` {Object}
  * `filename` {string} Specifies the filename used in stack traces produced
    by this script. **Default:** `''`.
  * `lineOffset` {number} Specifies the line number offset that is displayed
    in stack traces produced by this script. **Default:** `0`.
  * `columnOffset` {number} Specifies the column number offset that is displayed
    in stack traces produced by this script. **Default:** `0`.
  * `cachedData` {Buffer} Provides an optional `Buffer` with V8's code cache
    data for the supplied source.
  * `produceCachedData` {boolean} Specifies whether to produce new cache data.
    **Default:** `false`.
  * `parsingContext` {Object} The [contextified][] sandbox in which the said
    function should be compiled in.
  * `contextExtensions` {Object[]} An array containing a collection of context
    extensions (objects wrapping the current scope) to be applied while
    compiling. **Default:** `[]`.

Compiles the given code into the provided context/sandbox (if no context is
supplied, the current context is used), and returns it wrapped inside a
function with the given `params`.

