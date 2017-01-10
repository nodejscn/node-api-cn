
The filename extension of the compiled Addon binary is `.node` (as opposed
to `.dll` or `.so`). The [`require()`][require] function is written to look for
files with the `.node` file extension and initialize those as dynamically-linked
libraries.

When calling [`require()`][require], the `.node` extension can usually be
omitted and Node.js will still find and initialize the Addon. One caveat,
however, is that Node.js will first attempt to locate and load modules or
JavaScript files that happen to share the same base name. For instance, if
there is a file `addon.js` in the same directory as the binary `addon.node`,
then [`require('addon')`][require] will give precedence to the `addon.js` file
and load it instead.

