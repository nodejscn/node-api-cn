<!-- YAML
added: v0.7.7
-->

* {Object}

The `process.execArgv` property returns the set of Node.js-specific command-line
options passed when the Node.js process was launched. These options do not
appear in the array returned by the [`process.argv`][] property, and do not
include the Node.js executable, the name of the script, or any options following
the script name. These options are useful in order to spawn child processes with
the same execution environment as the parent.

For example:

```console
$ node --harmony script.js --version
```

Results in `process.execArgv`:

<!-- eslint-disable semi -->
```js
['--harmony']
```

And `process.argv`:

<!-- eslint-disable semi -->
```js
['/usr/local/bin/node', 'script.js', '--version']
```

