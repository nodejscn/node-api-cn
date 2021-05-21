<!-- YAML
added: v15.0.0
-->

* Type: {CryptoKey}

ECDH key derivation operates by taking as input one parties private key and
another parties public key -- using both to generate a common shared secret.
The `ecdhKeyDeriveParams.public` property is set to the other parties public
key.

