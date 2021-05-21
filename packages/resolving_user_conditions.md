<!-- YAML
added:
  - v14.9.0
  - v12.19.0
-->

When running Node.js, custom user conditions can be added with the
`--conditions` flag:

```bash
node --conditions=development main.js
```

which would then resolve the `"development"` condition in package imports and
exports, while resolving the existing `"node"`, `"default"`, `"import"`, and
`"require"` conditions as appropriate.

Any number of custom conditions can be set with repeat flags.

