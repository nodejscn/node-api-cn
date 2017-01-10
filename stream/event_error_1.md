<!-- YAML
added: v0.9.4
-->

* {Error}

The `'error'` event may be emitted by a Readable implementation at any time.
Typically, this may occur if the underlying stream in unable to generate data
due to an underlying internal failure, or when a stream implementation attempts
to push an invalid chunk of data.

The listener callback will be passed a single `Error` object.

