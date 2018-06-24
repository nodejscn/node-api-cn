<!-- YAML
added: v10.5.0
-->

* {null|stream.Writable}

If `stdin: true` was passed to the [`Worker`][] constructor, this is a
writable stream. The data written to this stream will be made available in
the worker thread as [`process.stdin`][].

