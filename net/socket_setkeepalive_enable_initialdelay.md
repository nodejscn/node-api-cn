<!-- YAML
added: v0.1.92
-->

* Returns: {net.Socket} The socket itself.

Enable/disable keep-alive functionality, and optionally set the initial
delay before the first keepalive probe is sent on an idle socket.
`enable` defaults to `false`.

Set `initialDelay` (in milliseconds) to set the delay between the last
data packet received and the first keepalive probe. Setting 0 for
initialDelay will leave the value unchanged from the default
(or previous) setting. Defaults to `0`.

