<!-- YAML
added:
  - v14.5.0
  - v12.19.0
-->

A message posted to a [`MessagePort`][] could not be deserialized in the target
[vm][] `Context`. Not all Node.js objects can be successfully instantiated in
any context at this time, and attempting to transfer them using `postMessage()`
can fail on the receiving side in that case.

<a id="ERR_METHOD_NOT_IMPLEMENTED"></a>
