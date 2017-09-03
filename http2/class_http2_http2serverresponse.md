<!-- YAML
added: v8.4.0
-->

This object is created internally by an HTTP server--not by the user. It is
passed as the second parameter to the [`'request'`][] event.

The response implements, but does not inherit from, the [Writable Stream][]
interface. This is an [`EventEmitter`][] with the following events:

