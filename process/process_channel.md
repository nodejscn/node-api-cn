<!-- YAML
added: v7.1.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30165
    description: The object no longer accidentally exposes native C++ bindings.
-->

* {Object}

如果 Node.js 进程是由 IPC 通道（参见[子进程][Child Process]文档）方式创建的，`process.channel` 属性保存 IPC 通道的引用。
如果 IPC 通道不存在，则此属性值为 `undefined`。
