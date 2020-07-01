<!-- YAML
added: v14.5.0
-->

* `type` {string}
* `listener` {Function|EventListener}
* `options` {Object}
  * `once` {boolean}

* Returns: {EventTarget} this

Node.js-specific extension to the `EventTarget` class that emulates the
equivalent `EventEmitter` API. The only difference between `addListener()` and
`addEventListener()` is that `addListener()` will return a reference to the
`EventTarget`.

