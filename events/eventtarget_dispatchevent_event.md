<!-- YAML
added: v14.5.0
-->

* `event` {Object|Event}

Dispatches the `event` to the list of handlers for `event.type`. The `event`
may be an `Event` object or any object with a `type` property whose value is
a `string`.

The registered event listeners is synchronously invoked in the order they
were registered.

