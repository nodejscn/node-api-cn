<!-- YAML
added: v11.8.0
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27312
    description: changed from `--diagnostic-report-on-signal` to
                 `--report-on-signal`
-->

Enables report to be generated upon receiving the specified (or predefined)
signal to the running Node.js process, if `--experimental-report` is enabled.
The signal to trigger the report is specified through `--report-signal`.

