<!-- YAML
added: v0.9.1
-->

* Returns: {net.Server}

与 `unref` 相反，在一个已经调用 `unref` 的 server 中调用 `ref`，如果 server 是仅存的 server，则程序不会退出（默认）。对一个已经调用 `ref` 的 server 再次调用 `ref` 将不会再有效果。
