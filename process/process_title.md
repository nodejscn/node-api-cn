<!-- YAML
added: v0.1.104
-->

* {string}

The `process.title` property returns the current process title (i.e. returns
the current value of `ps`). Assigning a new value to `process.title` modifies
the current value of `ps`.

*Note*: When a new value is assigned, different platforms will impose
different maximum length restrictions on the title. Usually such restrictions
are quite limited. For instance, on Linux and macOS, `process.title` is limited
to the size of the binary name plus the length of the command line arguments
because setting the `process.title` overwrites the `argv` memory of the
process.  Node.js v0.8 allowed for longer process title strings by also
overwriting the `environ` memory but that was potentially insecure and
confusing in some (rather obscure) cases.

