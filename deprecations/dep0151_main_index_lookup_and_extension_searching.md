<!-- YAML
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37206
    description: Runtime deprecation.
  - version: v15.8.0
    pr-url: https://github.com/nodejs/node/pull/36918
    description: Documentation-only deprecation
                 with `--pending-deprecation` support.
-->

Type: Runtime

Previously, `index.js` and extension searching lookups would apply to
`import 'pkg'` main entry point resolution, even when resolving ES modules.

With this deprecation, all ES module main entry point resolutions require
an explicit [`"exports"` or `"main"` entry][] with the exact file extension.

