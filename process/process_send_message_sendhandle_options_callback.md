<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {Handle object}
* `options` {Object}
* `callback` {Function}
* Returns: {boolean}

If Node.js is spawned with an IPC channel, the `process.send()` method can be
used to send messages to the parent process. Messages will be received as a
[`'message'`][] event on the parent's [`ChildProcess`][] object.

If Node.js was not spawned with an IPC channel, `process.send()` will be
`undefined`.

*Note*: The message goes through JSON serialization and parsing. The resulting
message might not be the same as what is originally sent. See notes in
[the `JSON.stringify()` specification][`JSON.stringify` spec].
