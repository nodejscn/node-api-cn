<!-- YAML
added: v0.4.0
-->

* Type: {string}

```json
{
  "main": "./main.js"
}
```

The `"main"` field defines the script that is used when the [package directory
is loaded via `require()`](modules.html#modules_folders_as_modules). Its value
is interpreted as a path.

```js
require('./path/to/directory'); // This resolves to ./path/to/directory/main.js.
```

When a package has an [`"exports"`][] field, this will take precedence over the
`"main"` field when importing the package by name.

