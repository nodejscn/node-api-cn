<!-- YAML
changes:
  - version: v15.13.0
    pr-url: https://github.com/nodejs/node/pull/37784
    description: Deprecation revoked. Status changed to "Legacy".
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22715
    description: Documentation-only deprecation.
-->

Type: Deprecation revoked

The [Legacy URL API][] is deprecated. This includes [`url.format()`][],
[`url.parse()`][], [`url.resolve()`][], and the [legacy `urlObject`][]. Please
use the [WHATWG URL API][] instead.

