
V8 调试器的集成允许将 Chrome 开发者工具附加到 Node.js 实例，以便进行调试和性能分析。 
它使用了 [Chrome 开发者工具协议][Chrome DevTools Protocol]。

可以通过在启动 Node.js 应用程序时传入 `--inspect` 标志来启用 V8 调试器。 
也可以使用该标志提供自定义的端口，例如 `--inspect=9222` 将会在 9222 端口上接受开发者工具的连接。

如果要在应用程序代码的第一行进行断点，则传入 `--inspect-brk` 标志而不是 `--inspect`。

```console
$ node --inspect index.js
Debugger listening on 127.0.0.1:9229.
To start debugging, open the following URL in Chrome:
    chrome-devtools://devtools/bundled/js_app.html?experiments=true&v8only=true&ws=127.0.0.1:9229/dc9010dd-f8b8-4ac5-a510-c1a114ec7d29
```

（在上面的示例中，URL 末尾的 UUID dc9010dd-f8b8-4ac5-a510-c1a114ec7d29 是动态生成的，它在不同的调试会话中是不一样的。）

如果 Chrome 浏览器的版本低于 66.0.3345.0，则在上述的 URL 中使用 `inspector.html` 而不是 `js_app.html`。

Chrome 开发者工具目前还不支持调试[工作线程][Worker Threads]。 
可以使用 [ndb] 来调试它们。

