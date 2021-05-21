<!-- YAML
added: v15.0.0
-->

* Type: {ArrayBuffer|TypedArray|DataView|Buffer}

The initialization vector must be unique for every encryption operation
using a given key. It is recommended by the AES-GCM specification that
this contain at least 12 random bytes.

