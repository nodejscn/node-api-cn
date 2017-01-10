<!-- YAML
added: v0.1.91
-->

* `preserveCursor` {Boolean}

The `replServer.displayPrompt()` method readies the REPL instance for input
from the user, printing the configured `prompt` to a new line in the `output`
and resuming the `input` to accept new input.

When multi-line input is being entered, an ellipsis is printed rather than the
'prompt'.

When `preserveCursor` is `true`, the cursor placement will not be reset to `0`.

The `replServer.displayPrompt` method is primarily intended to be called from
within the action function for commands registered using the
`replServer.defineCommand()` method.

