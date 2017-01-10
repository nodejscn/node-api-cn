<!-- YAML
added: v5.0.0
-->

Returns an object representing the type, name, and size of parameter of
an ephemeral key exchange in [Perfect Forward Secrecy][] on a client
connection. It returns an empty object when the key exchange is not
ephemeral. As this is only supported on a client socket; `null` is returned
if called on a server socket. The supported types are `'DH'` and `'ECDH'`. The
`name` property is available only when type is 'ECDH'.

For Example: `{ type: 'ECDH', name: 'prime256v1', size: 256 }`

