<!-- YAML
added: v8.3.0
changes:
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/33472
    description: The constructor now accepts an `options` object.
                 The single supported option is `timeout`.
-->

Create a new resolver.

* `options` {Object}
  * `timeout` {integer} Query timeout in milliseconds, or `-1` to use the
    default timeout.

