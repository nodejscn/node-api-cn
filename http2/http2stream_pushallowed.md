<!-- YAML
added: v8.4.0
-->

* Value: {boolean}

Read-only property mapped to the `SETTINGS_ENABLE_PUSH` flag of the remote
client's most recent `SETTINGS` frame. Will be `true` if the remote peer
accepts push streams, `false` otherwise. Settings are the same for every
`Http2Stream` in the same `Http2Session`.

