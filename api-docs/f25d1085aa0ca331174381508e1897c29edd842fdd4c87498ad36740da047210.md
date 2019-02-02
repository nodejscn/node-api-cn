
V8 检查器集成允许将 Chrome 开发者工具附加到 Node.js 实例以进行调试和性能分析。 
它使用 [Chrome开发者工具协议][Chrome DevTools Protocol]。

可以通过在启动 Node.js 应用程序时传入 `--inspect` 标志来启用 V8 检查器。 
也可以提供带有该标志的自定义端口，例如 `--inspect=9222` 将接受端口 9222 上的开发者工具连接。

要在应用代码的第一行断开，请传入 `--inspect-brk` 标志而不是 `--inspect`。

```txt
$ node --inspect index.js
Debugger listening on 127.0.0.1:9229.
To start debugging, open the following URL in Chrome:
    chrome-devtools://devtools/bundled/js_app.html?experiments=true&v8only=true&ws=127.0.0.1:9229/dc9010dd-f8b8-4ac5-a510-c1a114ec7d29
```

（在上面的示例中，URL 末尾的 UUID dc9010dd-f8b8-4ac5-a510-c1a114ec7d29 是动态生成的，它在不同的调试会话中会有所不同。）

如果 Chrome 浏览器的版本低于 66.0.3345.0，请在上述网址中使用 `inspector.html` 而不是 `js_app.html`。


