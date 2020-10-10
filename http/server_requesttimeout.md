<!-- YAML
added: v14.11.0
-->

* {number} **Default:** `0`

Sets the timeout value in milliseconds for receiving the entire request from
the client.

If the timeout expires, the server responds with status 408 without
forwarding the request to the request listener and then closes the connection.

It must be set to a non-zero value (e.g. 120 seconds) to proctect against
potential Denial-of-Service attacks in case the server is deployed without a
reverse proxy in front.

