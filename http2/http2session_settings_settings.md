<!-- YAML
added: v8.4.0
-->

* `settings` {[Settings Object][]}
* Returns {undefined}

Updates the current local settings for this `Http2Session` and sends a new
`SETTINGS` frame to the connected HTTP/2 peer.

Once called, the `http2session.pendingSettingsAck` property will be `true`
while the session is waiting for the remote peer to acknowledge the new
settings.

*Note*: The new settings will not become effective until the SETTINGS
acknowledgement is received and the `'localSettings'` event is emitted. It
is possible to send multiple SETTINGS frames while acknowledgement is still
pending.

