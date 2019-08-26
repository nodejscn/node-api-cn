<!-- YAML
added: v10.5.0
removed: v11.12.0
-->

There was an attempt to use a `MessagePort` instance in a closed
state, usually after `.close()` has been called.

<a id="ERR_HTTP2_FRAME_ERROR"></a>
