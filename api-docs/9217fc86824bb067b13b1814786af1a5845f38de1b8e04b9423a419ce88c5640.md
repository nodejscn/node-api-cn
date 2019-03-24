
Usage of `ECDH` with non-dynamically generated key pairs has been simplified.
Now, [`ecdh.setPrivateKey()`][] can be called with a preselected private key
and the associated public point (key) will be computed and stored in the object.
This allows code to only store and provide the private part of the EC key pair.
[`ecdh.setPrivateKey()`][] now also validates that the private key is valid for
the selected curve.

The [`ecdh.setPublicKey()`][] method is now deprecated as its inclusion in the
API is not useful. Either a previously stored private key should be set, which
automatically generates the associated public key, or [`ecdh.generateKeys()`][]
should be called. The main drawback of using [`ecdh.setPublicKey()`][] is that
it can be used to put the ECDH key pair into an inconsistent state.

