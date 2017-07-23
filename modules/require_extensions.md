<!-- YAML
added: v0.3.0
deprecated: v0.10.6
-->

> Stability: 0 - Deprecated

* {Object}

Instruct `require` on how to handle certain file extensions.

Process files with the extension `.sjs` as `.js`:

```js
require.extensions['.sjs'] = require.extensions['.js'];
```

**Deprecated**  In the past, this list has been used to load
non-JavaScript modules into Node.js by compiling them on-demand.
However, in practice, there are much better ways to do this, such as
loading modules via some other Node.js program, or compiling them to
JavaScript ahead of time.

Since the module system is locked, this feature will probably never go
away.  However, it may have subtle bugs and complexities that are best
left untouched.

Note that the number of file system operations that the module system
has to perform in order to resolve a `require(...)` statement to a
filename scales linearly with the number of registered extensions.

In other words, adding extensions slows down the module loader and
should be discouraged.

