<!-- YAML
added: v8.4.0
-->

Disables TLS renegotiation for this `TLSSocket` instance. Once called, attempts
to renegotiate will trigger an `'error'` event on the `TLSSocket`.

