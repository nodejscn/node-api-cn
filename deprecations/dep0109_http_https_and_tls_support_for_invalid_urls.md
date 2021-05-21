<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/36853
    description: End-of-Life.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/20270
    description: Runtime deprecation.
-->

Type: End-of-Life

Some previously supported (but strictly invalid) URLs were accepted through the
[`http.request()`][], [`http.get()`][], [`https.request()`][],
[`https.get()`][], and [`tls.checkServerIdentity()`][] APIs because those were
accepted by the legacy `url.parse()` API. The mentioned APIs now use the WHATWG
URL parser that requires strictly valid URLs. Passing an invalid URL is
deprecated and support will be removed in the future.

