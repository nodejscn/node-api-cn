<!-- YAML
added: v12.16.0
-->

Sets the resolution algorithm for resolving ES module specifiers. Valid options
are `explicit` and `node`.

The default is `explicit`, which requires providing the full path to a
module. The `node` mode will enable support for optional file extensions and
the ability to import a directory that has an index file.

Please see [customizing ESM specifier resolution][] for example usage.

