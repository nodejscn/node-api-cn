<!-- YAML
added: v11.8.0
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27312
    description: changed from `--diagnostic-report-on-fatalerror` to
                 `--report-on-fatalerror`
-->

Enables the report to be triggered on fatal errors (internal errors within
the Node.js runtime such as out of memory) that lead to termination of the
application, if `--experimental-report` is enabled. Useful to inspect various
diagnostic data elements such as heap, stack, event loop state, resource
consumption etc. to reason about the fatal error.

