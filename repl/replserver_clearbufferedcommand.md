<!-- YAML
added: v9.0.0
-->

The `replServer.clearBufferedCommand()` method clears any command that has been
buffered but not yet executed. This method is primarily intended to be
called from within the action function for commands registered using the
`replServer.defineCommand()` method.

