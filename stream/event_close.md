<!-- YAML
added: v0.9.4
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18438
    description: Add `emitClose` option to specify if `'close'` is emitted on
                 destroy.
-->

当流或其底层资源（比如文件描述符）被关闭时触发。
表明不会再触发其他事件，也不会再发生操作。

如果使用 `emitClose` 选项创建[可写流]，则它将会始终发出 `'close'` 事件。
