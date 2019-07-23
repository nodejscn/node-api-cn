<!-- YAML
added: v0.4.5
changes:
  - version: v2.5.0
    pr-url: https://github.com/nodejs/node/pull/2228
    description: parameter `maxCachedSessions` added to `options` for TLS
                 sessions reuse.
  - version: v5.3.0
    pr-url: https://github.com/nodejs/node/pull/4252
    description: support `0` `maxCachedSessions` to disable TLS session caching.
-->

HTTPS 的 [`Agent`] 对象，类似于 [`http.Agent`]。 
有关更多信息，请参阅 [`https.request()`]。

