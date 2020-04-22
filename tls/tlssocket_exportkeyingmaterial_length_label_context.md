<!-- YAML
added: v13.10.0
-->

* `length` {number} number of bytes to retrieve from keying material
* `label` {string} an application specific label, typically this will be a
value from the
[IANA Exporter Label Registry](https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#exporter-labels).
* `context` {Buffer} Optionally provide a context.

* Returns: {Buffer} requested bytes of the keying material

Keying material is used for validations to prevent different kind of attacks in
network protocols, for example in the specifications of IEEE 802.1X.

Example

```js
const keyingMaterial = tlsSocket.exportKeyingMaterial(
  128,
  'client finished');

/**
 Example return value of keyingMaterial:
 <Buffer 76 26 af 99 c5 56 8e 42 09 91 ef 9f 93 cb ad 6c 7b 65 f8 53 f1 d8 d9
    12 5a 33 b8 b5 25 df 7b 37 9f e0 e2 4f b8 67 83 a3 2f cd 5d 41 42 4c 91
    74 ef 2c ... 78 more bytes>
*/
```
See the OpenSSL [`SSL_export_keying_material`][] documentation for more
information.

