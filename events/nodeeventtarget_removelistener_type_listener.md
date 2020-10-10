<!-- YAML
added: v14.5.0
-->

* `type` {string}
* `listener` {Function|EventListener}

* Returns: {EventTarget} this

Node.js-specific extension to the `EventTarget` class that removes the
`listener` for the given `type`. The only difference between `removeListener()`
and `removeEventListener()` is that `removeListener()` will return a reference
to the `EventTarget`.



















