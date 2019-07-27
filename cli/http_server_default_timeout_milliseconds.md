<!-- YAML
added: v12.4.0
-->

Overrides the default value of `http`, `https` and `http2` server socket
timeout. Setting the value to 0 disables server socket timeout. Unless
provided, http server sockets timeout after 120s (2 minutes). Programmatic
setting of the timeout takes precedence over the value set through this
flag.

