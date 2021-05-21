<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37302
    description: Runtime deprecation.
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35562
    description: Runtime deprecation for permissive behavior.
  - version: v14.14.0
    pr-url: https://github.com/nodejs/node/pull/35579
    description: Documentation-only deprecation.
-->

Type: Runtime

In future versions of Node.js, `recursive` option will be ignored for
`fs.rmdir`, `fs.rmdirSync`, and `fs.promises.rmdir`.

Use `fs.rm(path, { recursive: true, force: true })`,
`fs.rmSync(path, { recursive: true, force: true })` or
`fs.promises.rm(path, { recursive: true, force: true })` instead.

