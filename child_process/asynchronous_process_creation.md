
The [`child_process.spawn()`][], [`child_process.fork()`][], [`child_process.exec()`][],
and [`child_process.execFile()`][] methods all follow the idiomatic asynchronous
programming pattern typical of other Node.js APIs.

Each of the methods returns a [`ChildProcess`][] instance. These objects
implement the Node.js [`EventEmitter`][] API, allowing the parent process to
register listener functions that are called when certain events occur during
the life cycle of the child process.

The [`child_process.exec()`][] and [`child_process.execFile()`][] methods additionally
allow for an optional `callback` function to be specified that is invoked
when the child process terminates.

