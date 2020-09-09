<!-- YAML
added: v0.1.25
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22715
    description: The Legacy URL API is deprecated. Use the WHATWG URL API.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8215
    description: The `auth` fields are now kept intact when `from` and `to`
                 refer to the same host.
  - version: v6.5.0, v4.6.2
    pr-url: https://github.com/nodejs/node/pull/8214
    description: The `port` field is copied correctly now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/1480
    description: The `auth` fields is cleared now the `to` parameter
                 contains a hostname.
-->

> Stability: 0 - Deprecated: Use the WHATWG URL API instead.

* `from` {string} The Base URL being resolved against.
* `to` {string} The HREF URL being resolved.

The `url.resolve()` method resolves a target URL relative to a base URL in a
manner similar to that of a Web browser resolving an anchor tag HREF.

```js
const url = require('url');
url.resolve('/one/two/three', 'four');         // '/one/two/four'
url.resolve('http://example.com/', '/one');    // 'http://example.com/one'
url.resolve('http://example.com/one', '/two'); // 'http://example.com/two'
```

<a id="whatwg-percent-encoding"></a>
