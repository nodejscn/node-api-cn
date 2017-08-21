
事件跟踪提供了一个机制，用于集中地跟踪 V8 引擎、Node 核心模块、以及用户代码产生的信息。

要启用事件跟踪，需在启动 Node.js 应用时传入 `--trace-events-enabled` 标记。

如果要指定跟踪的类别，可在 `--trace-event-categories` 标记后带上一个用逗号分隔的类别名称列表。
默认启用的类别是 `node` 和 `v8`。

```txt
node --trace-events-enabled --trace-event-categories v8,node server.js
```

启用事件跟踪模式运行 Node.js 时会产生日志文件，可以在 Chrome 浏览器的 [`chrome://tracing`] 标签中打开。
