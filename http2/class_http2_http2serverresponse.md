<!-- YAML
added: v8.4.0
-->

This object is created internally by an HTTP server — not by the user. It is
passed as the second parameter to the [`'request'`][] event.

The response inherits from [Stream][], and additionally implements the
following:

