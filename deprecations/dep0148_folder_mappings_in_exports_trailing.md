<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37215
    description: Runtime deprecation.
  - version: v15.1.0
    pr-url: https://github.com/nodejs/node/pull/35747
    description: Runtime deprecation for self-referencing imports.
  - version: v14.13.0
    pr-url: https://github.com/nodejs/node/pull/34718
    description: Documentation-only deprecation.
-->

Type: Runtime

Using a trailing `"/"` to define
[subpath folder mappings][] in the [subpath exports][] or
[subpath imports][] fields is deprecated. Use [subpath patterns][] instead.

