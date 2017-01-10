
**NOTE: This is an experimental feature.**

V8 Inspector integration allows attaching Chrome DevTools to Node.js
instances for debugging and profiling.

V8 Inspector can be enabled by passing the `--inspect` flag when starting a
Node.js application. It is also possible to supply a custom port with that flag,
e.g. `--inspect=9222` will accept DevTools connections on port 9222.

To break on the first line of the application code, provide the `--debug-brk`
flag in addition to `--inspect`.

```txt
$ node --inspect index.js
Debugger listening on port 9229.
Warning: This is an experimental feature and could change at any time.
To start debugging, open the following URL in Chrome:
    chrome-devtools://devtools/remote/serve_file/@60cd6e859b9f557d2312f5bf532f6aec5f284980/inspector.html?experiments=true&v8only=true&ws=localhost:9229/node
```

[TCP-based protocol]: https://github.com/v8/v8/wiki/Debugging-Protocol
