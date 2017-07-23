<!-- YAML
added: 8.2.0
-->

* {integer} The largest size allowed for a single `Buffer` instance

On 32-bit architectures, this value is `(2^30)-1` (~1GB).
On 64-bit architectures, this value is `(2^31)-1` (~2GB).

This value is also available as [`buffer.kMaxLength`][].

