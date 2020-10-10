<!-- YAML
added: v8.4.0
-->

* `settings` {HTTP/2 Settings Object}
* `callback` {Function} Callback that is called once the session is connected or
  right away if the session is already connected.
  * `err` {Error|null}
  * `settings` {HTTP/2 Settings Object} The updated `settings` object.
  * `duration` {integer}

Updates the current local settings for this `Http2Session` and sends a new
`SETTINGS` frame to the connected HTTP/2 peer.

Once called, the `http2session.pendingSettingsAck` property will be `true`
while the session is waiting for the remote peer to acknowledge the new
settings.

The new settings will not become effective until the `SETTINGS` acknowledgment
is received and the `'localSettings'` event is emitted. It is possible to send
multiple `SETTINGS` frames while acknowledgment is still pending.

