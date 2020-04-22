<!-- YAML
changes:
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/29061
-->

Type: Runtime

[`WriteStream.open()`][] and [`ReadStream.open()`][] are undocumented internal
APIs that do not make sense to use in userland. File streams should always be
opened through their corresponding factory methods [`fs.createWriteStream()`][]
and [`fs.createReadStream()`][]) or by passing a file descriptor in options.

<a id="DEP0136"></a>
