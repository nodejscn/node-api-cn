<!-- YAML
added: v0.9.4
-->

* {Error}

The `'error'` event is emitted if an error occurred while writing or piping
data. The listener callback is passed a single `Error` argument when called.

*Note*: The stream is not closed when the `'error'` event is emitted.

