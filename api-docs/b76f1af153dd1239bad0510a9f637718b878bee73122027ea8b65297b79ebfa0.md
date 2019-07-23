<!-- YAML
changes:
  - version: v12.5.0
    pr-url: https://github.com/nodejs/node/pull/28209
    description: do not automatically set servername if the target host was
                 specified using an IP address.
-->
* `options` {Object} 在代理上设置的一组可配置的选项。可以具有与 [`http.Agent(options)`] 相同的字段，以及：
  * `maxCachedSessions` {number} TLS 缓存会话的最大数量。使用 `0` 可禁用 TLS 会话缓存。**默认值:** `100`。
  * `servername` {string} 要发送到服务器的[服务器名称指示的扩展名][sni wiki]的值。使用空字符串 `''` 可以禁用发送扩展名。**默认值：** 目标服务器的主机名，除非目标服务器被指定为使用 IP 地址，在这种情况下默认为 `''`（无扩展名）。

    有关 TLS 会话复用的信息，请参阅[会话恢复][`Session Resumption`]。

