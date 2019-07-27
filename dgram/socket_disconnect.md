<!-- YAML
added: v12.0.0
-->

A synchronous function that disassociates a connected `dgram.Socket` from
its remote address. Trying to call `disconnect()` on an already disconnected
socket will result in an [`ERR_SOCKET_DGRAM_NOT_CONNECTED`][] exception.

