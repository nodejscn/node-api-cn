<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/24862
    description: End-of-Life.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22485
    description: Runtime deprecation.
-->

Type: End-of-Life

Windows Performance Counter support has been removed from Node.js. The
undocumented `COUNTER_NET_SERVER_CONNECTION()`,
`COUNTER_NET_SERVER_CONNECTION_CLOSE()`, `COUNTER_HTTP_SERVER_REQUEST()`,
`COUNTER_HTTP_SERVER_RESPONSE()`, `COUNTER_HTTP_CLIENT_REQUEST()`, and
`COUNTER_HTTP_CLIENT_RESPONSE()` functions have been deprecated.

<a id="DEP0121"></a>
