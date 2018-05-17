<!-- YAML
added: v9.7.0
-->

* Returns: {Immediate} a reference to `immediate`

When called, requests that the Node.js event loop *not* exit so long as the
`Immediate` is active. Calling `immediate.ref()` multiple times will have no
effect.

By default, all `Immediate` objects are "ref'ed", making it normally unnecessary
to call `immediate.ref()` unless `immediate.unref()` had been called previously.

