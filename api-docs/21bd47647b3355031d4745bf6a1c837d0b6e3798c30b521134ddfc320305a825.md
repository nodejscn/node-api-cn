<!-- YAML
changes:
  - version: v10.15.0
    pr-url: https://github.com/nodejs/node/commit/186035243fad247e3955f
    description: Max header size in `http_parser` was set to 8KB.
-->

Too much HTTP header data was received. In order to protect against malicious or
malconfigured clients, if more than 8KB of HTTP header data is received then
HTTP parsing will abort without a request or response object being created, and
an `Error` with this code will be emitted.

<a id="MODULE_NOT_FOUND"></a>
