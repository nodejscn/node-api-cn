<!-- YAML
added: v0.4.5
changes:
  - version: v5.3.0
    pr-url: https://github.com/nodejs/node/pull/4252
    description: 支持 `maxCachedSessions` 为 `0`，用于禁用 TLS 会话的缓存。
  - version: v2.5.0
    pr-url: https://github.com/nodejs/node/pull/2228
    description: 新增 `maxCachedSessions` 参数到 `options`，用于 TLS 会话的再利用。
-->

HTTPS 的 [`Agent`] 对象，类似于 [`http.Agent`]。 
有关更多信息，请参见 [`https.request()`]。

