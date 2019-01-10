<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19414
    description: Documentation-only deprecation.
-->

Type: Documentation-only

Deprecated alias for [`zlib.bytesWritten`][]. This original name was chosen
because it also made sense to interpret the value as the number of bytes
read by the engine, but is inconsistent with other streams in Node.js that
expose values under these names.

<a id="DEP0110"></a>
