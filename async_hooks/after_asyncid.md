
* `asyncId` {number}

Called immediately after the callback specified in `before` is completed.

*Note:* If an uncaught exception occurs during execution of the callback then
`after` will run after the `'uncaughtException'` event is emitted or a
`domain`'s handler runs.


