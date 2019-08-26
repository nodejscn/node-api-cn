
> Stability: 1 - Experimental

The `--entry-type=commonjs` flag was used to attempt to execute an `.mjs` file
or a `.js` file where the nearest parent `package.json` contains
`"type": "module"`; or
the `--entry-type=module` flag was used to attempt to execute a `.cjs` file or
a `.js` file where the nearest parent `package.json` either lacks a `"type"`
field or contains `"type": "commonjs"`.

<a id="ERR_FS_WATCHER_ALREADY_STARTED"></a>
