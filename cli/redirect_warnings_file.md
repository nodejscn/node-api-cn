<!-- YAML
added: v8.0.0
-->

Write process warnings to the given file instead of printing to stderr. The
file will be created if it does not exist, and will be appended to if it does.
If an error occurs while attempting to write the warning to the file, the
warning will be written to stderr instead.

The `file` name may be an absolute path. If it is not, the default directory it
will be written to is controlled by the
[--diagnostic-dir](#cli_diagnostic_dir_directory) command-line option.

