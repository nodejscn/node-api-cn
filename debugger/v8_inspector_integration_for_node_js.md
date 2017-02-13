
**注意：这是一个试验的特性。**

V8 的检查器集成可以附加 Chrome 的开发者工具到 Node.js 实例以用于调试和性能分析。

当启动一个 Node.js 应用时，V8 检查器可以通过传入 `--inspect` 标志启用。
也可以通过该标志提供一个自定义的端口，如 `--inspect=9222` 会在 9222 端口接受开发者工具连接。

要想在应用代码的第一行断开，可以在除 `--inspect` 之外再提供 `--debug-brk` 标志。

```txt
$ node --inspect index.js
Debugger listening on port 9229.
Warning: This is an experimental feature and could change at any time.
To start debugging, open the following URL in Chrome:
    chrome-devtools://devtools/remote/serve_file/@60cd6e859b9f557d2312f5bf532f6aec5f284980/inspector.html?experiments=true&v8only=true&ws=localhost:9229/node
```

