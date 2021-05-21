<!-- YAML
added: v11.8.0
changes:
  - version:
     - v13.12.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/32242
    description: This option is no longer experimental.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27312
    description: changed from `--diagnostic-report-signal` to
                 `--report-signal`.
-->

Sets or resets the signal for report generation (not supported on Windows).
Default signal is `SIGUSR2`.

