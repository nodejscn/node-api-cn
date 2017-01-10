<!-- YAML
added: v0.1.98
-->

* `data` {String}
* `key` {Object}
  * `ctrl` {boolean} `true` to indicate the `<ctrl>` key.
  * `meta` {boolean} `true` to indicate the `<Meta>` key.
  * `shift` {boolean} `true` to indicate the `<Shift>` key.
  * `name` {String} The name of the a key.

The `rl.write()` method will write either `data` or a key sequence  identified
by `key` to the `output`. The `key` argument is supported only if `output` is
a [TTY][] text terminal.

If `key` is specified, `data` is ignored.

When called, `rl.write()` will resume the `input` stream if it has been
paused.

If the `readline.Interface` was created with `output` set to `null` or
`undefined` the `data` and `key` are not written.

For example:

```js
rl.write('Delete this!');
// Simulate Ctrl+u to delete the line written previously
rl.write(null, {ctrl: true, name: 'u'});
```

*Note*: The `rl.write()` method will write the data to the `readline`
Interface's `input` *as if it were provided by the user*.

