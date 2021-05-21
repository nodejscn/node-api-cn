<!-- YAML
added: v13.0.0
-->

* {boolean}

Readonly, `true` if `outgoingMessage.end()` has been called. Noted that
this property does not reflect whether the data has been flush. For that
purpose, use `message.writableFinished` instead.

