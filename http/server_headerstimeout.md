<!-- YAML
added: v10.14.0
-->

* {number} **Default:** `40000`

Limit the amount of time the parser will wait to receive the complete HTTP
headers.

In case of inactivity, the rules defined in [server.timeout][] apply. However,
that inactivity based timeout would still allow the connection to be kept open
if the headers are being sent very slowly (by default, up to a byte per 2
minutes). In order to prevent this, whenever header data arrives an additional
check is made that more than `server.headersTimeout` milliseconds has not
passed since the connection was established. If the check fails, a `'timeout'`
event is emitted on the server object, and (by default) the socket is destroyed.
See [server.timeout][] for more information on how timeout behaviour can be
customised.

