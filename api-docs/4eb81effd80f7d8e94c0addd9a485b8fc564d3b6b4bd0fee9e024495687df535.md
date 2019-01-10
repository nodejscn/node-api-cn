<!-- YAML
added: v10.11.0
-->

* {boolean}

Set the `true` if the `END_STREAM` flag was set in the request or response
HEADERS frame received, indicating that no additional data should be received
and the readable side of the `Http2Stream` will be closed.

