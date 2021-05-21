<!-- YAML
added: v9.0.0
-->

Overrides the pipe method of legacy `Stream` which is the parent class of
`http.outgoingMessage`.

Since `OutgoingMessage` should be a write-only stream,
call this function will throw an `Error`. Thus, it disabled the pipe method
it inherits from `Stream`.

The User should not call this function directly.

