<!-- YAML
added: v8.4.0
-->

The `'timeout'` event is emitted when there is no activity on the Server for
a given number of milliseconds set using `http2server.setTimeout()`.
**Default:** 2 minutes.

To change the default timeout use the [`--http-server-default-timeout`][]
flag.

