<!-- YAML
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/23020
    description: 除了 V8 选项，下划线（而不是短横线）现在也被允许用于 Node.js 选项。
-->

所有的选项，包括 V8 选项，允许单词被短横线（`-`）和下划线（`_`）分隔。
例如，`--pending-deprecation` 等效于 `--pending_deprecation`.。

如果一个接受一个值的选项（例如 `--max-http-header-size`）被传入超过一次，则最后一个传入的值被使用。 
命令行中的选项优先于通过 [`NODE_OPTIONS`] 环境变量传入的选项。

