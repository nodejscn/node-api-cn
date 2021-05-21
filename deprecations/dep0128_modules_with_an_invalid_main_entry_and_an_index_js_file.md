<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37204
    description: Runtime deprecation.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26823
    description: Documentation-only.
-->

Type: Runtime

Modules that have an invalid `main` entry (e.g., `./does-not-exist.js`) and
also have an `index.js` file in the top level directory will resolve the
`index.js` file. That is deprecated and is going to throw an error in future
Node.js versions.

