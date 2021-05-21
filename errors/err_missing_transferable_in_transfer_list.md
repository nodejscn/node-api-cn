<!-- YAML
added: v15.0.0
-->

An object that needs to be explicitly listed in the `transferList` argument
is in the object passed to a [`postMessage()`][] call, but is not provided
in the `transferList` for that call. Usually, this is a `MessagePort`.

In Node.js versions prior to v15.0.0, the error code being used here was
[`ERR_MISSING_MESSAGE_PORT_IN_TRANSFER_LIST`][]. However, the set of
transferable object types has been expanded to cover more types than
`MessagePort`.

<a id="ERR_MODULE_NOT_FOUND"></a>
