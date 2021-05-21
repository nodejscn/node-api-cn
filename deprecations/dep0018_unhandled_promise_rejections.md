<!-- YAML
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35316
    description: End-of-Life.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8217
    description: Runtime deprecation.
-->

Type: End-of-Life

Unhandled promise rejections are deprecated. By default, promise rejections
that are not handled terminate the Node.js process with a non-zero exit
code. To change the way Node.js treats unhandled rejections, use the
[`--unhandled-rejections`][] command-line option.

