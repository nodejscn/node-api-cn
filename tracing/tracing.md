
Trace 事件提供了一种机制，可以集中由 V8，Node 核心， 以及用户代码生成的跟踪信息。

启动 Node.js 应用时添加 `--trace-events-enabled` 标记，可以启用 Tracing.

可以通过在 `--trace-event-categories` 标记后跟一个用逗号分隔的类别名称列表, 来指定特定的跟踪记录集合。
`node` 和 `v8` 默认启用。

```txt
node --trace-events-enabled --trace-event-categories v8,node server.js
```

启用跟踪模式运行 Node.js 时会产生日志文件，可以在 [`chrome://tracing`](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool) 标签中打开。
