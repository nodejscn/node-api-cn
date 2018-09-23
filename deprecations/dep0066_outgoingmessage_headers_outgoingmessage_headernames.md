<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10941
    description: Documentation-only deprecation.
-->

Type: Documentation-only

The `http` module `outgoingMessage._headers` and `outgoingMessage._headerNames`
properties are deprecated. Use one of the public methods
(e.g. `outgoingMessage.getHeader()`, `outgoingMessage.getHeaders()`,
`outgoingMessage.getHeaderNames()`, `outgoingMessage.hasHeader()`,
`outgoingMessage.removeHeader()`, `outgoingMessage.setHeader()`) for working
with outgoing headers.

The `outgoingMessage._headers` and `outgoingMessage._headerNames` properties
were never documented as officially supported properties.

<a id="DEP0067"></a>
