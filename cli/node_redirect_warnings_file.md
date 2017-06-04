<!-- YAML
added: v8.0.0
-->

When set, process warnings will be emitted to the given file instead of
printing to stderr. The file will be created if it does not exist, and will be
appended to if it does. If an error occurs while attempting to write the
warning to the file, the warning will be written to stderr instead. This is
equivalent to using the `--redirect-warnings=file` command-line flag.

[`--openssl-config`]: #cli_openssl_config_file
[Buffer]: buffer.html#buffer_buffer
[Chrome Debugging Protocol]: https://chromedevtools.github.io/debugger-protocol-viewer
[REPL]: repl.html
[SlowBuffer]: buffer.html#buffer_class_slowbuffer
[debugger]: debugger.html
[emit_warning]: process.html#process_process_emitwarning_warning_name_ctor
