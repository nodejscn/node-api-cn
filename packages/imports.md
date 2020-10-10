<!-- YAML
added: v14.6.0
-->

> Stability: 1 - Experimental

* Type: {Object}

In addition to the [`"exports"`][] field it is possible to define internal
package import maps that only apply to import specifiers from within the package
itself.

Entries in the imports field must always start with `#` to ensure they are
clearly disambiguated from package specifiers.

For example, the imports field can be used to gain the benefits of conditional
exports for internal modules:

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

where `import '#dep'` would now get the resolution of the external package
`dep-node-native` (including its exports in turn), and instead get the local
file `./dep-polyfill.js` relative to the package in other environments.

Unlike the `"exports"` field, import maps permit mapping to external packages,
providing an important use case for conditional loading scenarios.

Apart from the above, the resolution rules for the imports field are otherwise
analogous to the exports field.



















