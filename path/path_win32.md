<!-- YAML
added: v0.11.15
-->

* {Object}

The `path.win32` property provides access to Windows-specific implementations
of the `path` methods.

*Note*: On Windows, both the forward slash (`/`) and backward slash (`\`)
characters are accepted as path delimiters; however, only the backward slash
(`\`) will be used in return values.

[`path.posix`]: #path_path_posix
[`path.win32`]: #path_path_win32
[`path.parse()`]: #path_path_parse_path
[`TypeError`]: errors.html#errors_class_typeerror
