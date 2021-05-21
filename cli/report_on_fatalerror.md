<!-- YAML
added: v11.8.0
changes:
  - version:
    - v14.0.0
    - v13.14.0
    - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/32496
    description: This option is no longer experimental.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27312
    description: changed from `--diagnostic-report-on-fatalerror` to
                 `--report-on-fatalerror`.
-->

Enables the report to be triggered on fatal errors (internal errors within
the Node.js runtime such as out of memory) that lead to termination of the
application. Useful to inspect various diagnostic data elements such as heap,
stack, event loop state, resource consumption etc. to reason about the fatal
error.

