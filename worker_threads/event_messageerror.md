<!-- YAML
added:
  - v14.5.0
  - v12.19.0
-->

* `error` {Error} An Error object

The `'messageerror'` event is emitted when deserializing a message failed.

Currently, this event is emitted when there is an error occurring while
instantiating the posted JS object on the receiving end. Such situations
are rare, but can happen, for instance, when certain Node.js API objects
are received in a `vm.Context` (where Node.js APIs are currently
unavailable).

