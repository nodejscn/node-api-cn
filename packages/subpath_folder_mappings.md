<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37215
    description: Runtime deprecation.
  - version: v15.1.0
    pr-url: https://github.com/nodejs/node/pull/35747
    description: Runtime deprecation for self-referencing imports.
  - version:
    - v14.13.0
    - v12.20.0
    pr-url: https://github.com/nodejs/node/pull/34718
    description: Documentation-only deprecation.
-->

> Stability: 0 - Deprecated: Use subpath patterns instead.

Before subpath patterns were supported, a trailing `"/"` suffix was used to
support folder mappings:

```json
{
  "exports": {
    "./features/": "./features/"
  }
}
```

_This feature will be removed in a future release._

Instead, use direct [subpath patterns][]:

```json
{
  "exports": {
    "./features/*": "./features/*.js"
  }
}
```

The benefit of patterns over folder exports is that packages can always be
imported by consumers without subpath file extensions being necessary.

