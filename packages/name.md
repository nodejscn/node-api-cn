<!-- YAML
added:
  - v12.16.0
  - v13.1.0
changes:
  - version:
    - v12.16.0
    - v13.6.0
    pr-url: https://github.com/nodejs/node/pull/31002
    description: Remove the `--experimental-resolve-self` option.
-->

* Type: {string}

```json
{
  "name": "package-name"
}
```

The `"name"` field defines your package’s name. Publishing to the
_npm_ registry requires a name that satisfies
[certain requirements](https://docs.npmjs.com/files/package.json#name).

The `"name"` field can be used in addition to the [`"exports"`][] field to
[self-reference][] a package using its name.

