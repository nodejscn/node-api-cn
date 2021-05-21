<!-- YAML
added: v15.0.0
-->

* Type: {ArrayBuffer|TypedArray|DataView|Buffer}

The initial value of the counter block. This must be exactly 16 bytes long.

The `AES-CTR` method uses the rightmost `length` bits of the block as the
counter and the remaining bits as the nonce.

