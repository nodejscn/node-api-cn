<!-- YAML
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8217
    description: Runtime deprecation.
-->

Type: Runtime

Unhandled promise rejections are deprecated. In the future, promise rejections
that are not handled will terminate the Node.js process with a non-zero exit
code.

