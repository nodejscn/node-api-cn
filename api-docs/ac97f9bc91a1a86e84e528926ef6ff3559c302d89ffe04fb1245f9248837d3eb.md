<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17141
    description: End-of-Life.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/14449
    description: Runtime deprecation.
-->

Type: End-of-Life

Accessing several internal, undocumented properties of `net.Server` instances
with inappropriate names is deprecated.

As the original API was undocumented and not generally useful for non-internal
code, no replacement API is provided.

<a id="DEP0074"></a>
