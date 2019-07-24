<!-- YAML
added: v10.5.0
-->

Disables further sending of messages on either side of the connection.
This method can be called when no further communication will happen over this
`MessagePort`.

The [`'close'` event][] will be emitted on both `MessagePort` instances that
are part of the channel.

