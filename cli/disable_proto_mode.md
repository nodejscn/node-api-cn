<!-- YAML
added:
 - v13.12.0
 - v12.17.0
-->

Disable the `Object.prototype.__proto__` property. If `mode` is `delete`, the
property is removed entirely. If `mode` is `throw`, accesses to the
property throw an exception with the code `ERR_PROTO_ACCESS`.

