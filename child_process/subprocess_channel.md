<!-- YAML
added: v7.1.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30165
    description: The object no longer accidentally exposes native C++ bindings.
-->

* {Object} 一个管道，表示子进程的 IPC 通道。

`subprocess.channel` 属性是对子进程的 IPC 通道的引用。
如果当前没有 IPC 通道，则此属性为 `undefined`。

