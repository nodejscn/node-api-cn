<!-- YAML
added: v11.13.0
-->

* `port` {MessagePort} The message port to transfer.
* `contextifiedSandbox` {Object} A [contextified][] object as returned by the
  `vm.createContext()` method.

* Returns: {MessagePort}

Transfer a `MessagePort` to a different [`vm`][] Context. The original `port`
object is rendered unusable, and the returned `MessagePort` instance
takes its place.

The returned `MessagePort` is an object in the target context and
inherits from its global `Object` class. Objects passed to the
[`port.onmessage()`][] listener are also created in the target context
and inherit from its global `Object` class.

However, the created `MessagePort` no longer inherits from
[`EventTarget`][], and only [`port.onmessage()`][] can be used to receive
events using it.

