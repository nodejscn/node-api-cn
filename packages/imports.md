<!-- YAML
added:
 - v14.6.0
 - v12.19.0
-->

* Type: {Object}

```json
// package.json
{
  "imports": {
    "#dep": {
      "node": "dep-node-native",
      "default": "./dep-polyfill.js"
    }
  },
  "dependencies": {
    "dep-node-native": "^1.0.0"
  }
}
```

Entries in the imports field must be strings starting with `#`.

Import maps permit mapping to external packages.

This field defines [subpath imports][] for the current package.






















