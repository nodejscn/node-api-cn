<!-- YAML
added: v12.0.0
-->

* Returns: {Object}

Returns an object containing the `address`, `family`, and `port` of the remote
endpoint. This method throws an [`ERR_SOCKET_DGRAM_NOT_CONNECTED`][] exception
if the socket is not connected.

