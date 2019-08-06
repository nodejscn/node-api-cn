<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23329
    description: Runtime deprecation.
-->

Type: Runtime

Setting the TLS ServerName to an IP address is not permitted by
[RFC 6066][]. This will be ignored in a future version.

<a id="DEP0124"></a>
