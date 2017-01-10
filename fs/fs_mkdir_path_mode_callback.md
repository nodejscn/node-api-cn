<!-- YAML
added: v0.1.8
-->

* `path` {String | Buffer}
* `mode` {Integer}
* `callback` {Function}

Asynchronous mkdir(2). No arguments other than a possible exception are given
to the completion callback. `mode` defaults to `0o777`.

