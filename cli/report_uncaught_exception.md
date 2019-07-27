<!-- YAML
added: v11.8.0
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27312
    description: changed from `--diagnostic-report-uncaught-exception` to
                 `--report-uncaught-exception`
-->

Enables report to be generated on un-caught exceptions, if
`--experimental-report` is enabled. Useful when inspecting JavaScript stack in
conjunction with native stack and other runtime environment data.

