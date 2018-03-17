定制一个默认的模块解决方案，加载钩子能通过提供给Node一个 `--loader ./loader-name.mjs` 参数来配置。

当钩子被使用时，只支持ES模块加载，不支持任何的CommonJS模块加载。
<!-- type=misc -->

To customize the default module resolution, loader hooks can optionally be
provided via a `--loader ./loader-name.mjs` argument to Node.

When hooks are used they only apply to ES module loading and not to any
CommonJS modules loaded.

