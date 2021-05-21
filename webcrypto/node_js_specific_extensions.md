
The Node.js Web Crypto API extends various aspects of the Web Crypto API.
These extensions are consistently identified by prepending names with the
`node.` prefix. For instance, the `'node.keyObject'` key format can be
used with the `subtle.exportKey()` and `subtle.importKey()` methods to
convert between a WebCrypto {CryptoKey} object and a Node.js {KeyObject}.

Care should be taken when using Node.js-specific extensions as they are
not supported by other WebCrypto implementations and reduce the portability
of code to other environments.

