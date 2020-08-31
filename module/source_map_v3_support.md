<!-- YAML
added:
 - v13.7.0
 - v12.17.0
-->

> Stability: 1 - Experimental

Helpers for interacting with the source map cache. This cache is
populated when source map parsing is enabled and
[source map include directives][] are found in a modules' footer.

To enable source map parsing, Node.js must be run with the flag
[`--enable-source-maps`][], or with code coverage enabled by setting
[`NODE_V8_COVERAGE=dir`][].

```js
const { findSourceMap, SourceMap } = require('module');
```

