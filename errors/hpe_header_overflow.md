<!-- YAML
changes:
  - version:
     - v11.4.0
     - v10.15.0
    commit: 186035243fad247e3955f
    pr-url: https://github.com/nodejs-private/node-private/pull/143
    description: Max header size in `http_parser` was set to 8KB.
-->

Too much HTTP header data was received. In order to protect against malicious or
malconfigured clients, if more than 8KB of HTTP header data is received then
HTTP parsing will abort without a request or response object being created, and
an `Error` with this code will be emitted.

<a id="HPE_UNEXPECTED_CONTENT_LENGTH"></a>
