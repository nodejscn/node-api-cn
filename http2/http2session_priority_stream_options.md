<!-- YAML
added: v8.4.0
-->

* `stream` {Http2Stream}
* `options` {Object}
  * `exclusive` {boolean} When `true` and `parent` identifies a parent Stream,
    the given stream is made the sole direct dependency of the parent, with
    all other existing dependents made a dependent of the given stream. Defaults
    to `false`.
  * `parent` {number} Specifies the numeric identifier of a stream the given
    stream is dependent on.
  * `weight` {number} Specifies the relative dependency of a stream in relation
    to other streams with the same `parent`. The value is a number between `1`
    and `256` (inclusive).
  * `silent` {boolean} When `true`, changes the priority locally without
    sending a `PRIORITY` frame to the connected peer.
* Returns: {undefined}

Updates the priority for the given `Http2Stream` instance.

