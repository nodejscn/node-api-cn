<!-- YAML
added: v8.4.0
-->

* `headers` {Object}

This method adds HTTP trailing headers (a header but at the end of the
message) to the response.

Attempting to set a header field name or value that contains invalid characters
will result in a [`TypeError`][] being thrown.

