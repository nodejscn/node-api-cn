<!-- YAML
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/23020
    description: Underscores instead of dashes are now allowed for
                 Node.js options as well, in addition to V8 options.
-->

所有选项（包括 V8 选项）都允许单词用短划线（`-`）或下划线（`_`）分隔。
例如，`--pending-deprecation` 等效于 `--pending_deprecation`。

If an option that takes a single value (such as `--max-http-header-size`) is
passed more than once, then the last passed value is used. Options from the
command line take precedence over options passed through the [`NODE_OPTIONS`][]
environment variable.

