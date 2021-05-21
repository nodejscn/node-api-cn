<!-- YAML
added: v14.5.0
-->

* `type` {string}
* `listener` {Function|EventListener}
* `options` {Object}
  * `once` {boolean} When `true`, the listener is automatically removed
    when it is first invoked. **Default:** `false`.
  * `passive` {boolean} When `true`, serves as a hint that the listener will
    not call the `Event` object's `preventDefault()` method.
    **Default:** `false`.
  * `capture` {boolean} Not directly used by Node.js. Added for API
    completeness. **Default:** `false`.

Adds a new handler for the `type` event. Any given `listener` is added
only once per `type` and per `capture` option value.

If the `once` option is `true`, the `listener` is removed after the
next time a `type` event is dispatched.

The `capture` option is not used by Node.js in any functional way other than
tracking registered event listeners per the `EventTarget` specification.
Specifically, the `capture` option is used as part of the key when registering
a `listener`. Any individual `listener` may be added once with
`capture = false`, and once with `capture = true`.

```js
function handler(event) {}

const target = new EventTarget();
target.addEventListener('foo', handler, { capture: true });  // first
target.addEventListener('foo', handler, { capture: false }); // second

// Removes the second instance of handler
target.removeEventListener('foo', handler);

// Removes the first instance of handler
target.removeEventListener('foo', handler, { capture: true });
```

