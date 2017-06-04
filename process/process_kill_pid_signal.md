<!-- YAML
added: v0.0.6
-->

* `pid` {number} A process ID
* `signal` {string|number} The signal to send, either as a string or number.
  Defaults to `'SIGTERM'`.

The `process.kill()` method sends the `signal` to the process identified by
`pid`.

Signal names are strings such as `'SIGINT'` or `'SIGHUP'`. See [Signal Events][]
and kill(2) for more information.

This method will throw an error if the target `pid` does not exist. As a special
case, a signal of `0` can be used to test for the existence of a process.
Windows platforms will throw an error if the `pid` is used to kill a process
group.

*Note*: Even though the name of this function is `process.kill()`, it is
really just a signal sender, like the `kill` system call.  The signal sent may
do something other than kill the target process.

For example:

```js
process.on('SIGHUP', () => {
  console.log('Got SIGHUP signal.');
});

setTimeout(() => {
  console.log('Exiting.');
  process.exit(0);
}, 100);

process.kill(process.pid, 'SIGHUP');
```

*Note*: When `SIGUSR1` is received by a Node.js process, Node.js will start
the debugger, see [Signal Events][].

