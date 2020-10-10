<!-- YAML
added: v11.13.0
-->

* `port` {MessagePort} The message port which will be transferred.
* `contextifiedSandbox` {Object} A [contextified][] object as returned by the
  `vm.createContext()` method.

* Returns: {MessagePort}

Transfer a `MessagePort` to a different [`vm`][] Context. The original `port`
object will be rendered unusable, and the returned `MessagePort` instance will
take its place.

The returned `MessagePort` will be an object in the target context, and will
inherit from its global `Object` class. Objects passed to the
[`port.onmessage()`][] listener will also be created in the target context
and inherit from its global `Object` class.

However, the created `MessagePort` will no longer inherit from
[`EventEmitter`][], and only [`port.onmessage()`][] can be used to receive
events using it.

