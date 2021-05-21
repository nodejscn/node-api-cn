<!-- YAML
changes:
  - version: v15.13.0
    pr-url: https://github.com/nodejs/node/pull/37784
    description: Deprecation revoked. Status changed to "Legacy".
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22715
    description: The Legacy URL API is deprecated. Use the WHATWG URL API.
-->

> Stability: 3 - Legacy: Use the WHATWG URL API instead.

The legacy `urlObject` (`require('url').Url`) is created and returned by the
`url.parse()` function.

