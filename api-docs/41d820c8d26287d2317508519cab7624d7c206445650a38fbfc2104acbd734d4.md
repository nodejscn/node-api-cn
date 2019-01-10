<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: End-of-Life.
-->

Type: End-of-Life

Using the `noAssert` argument has no functionality anymore. All input is going
to be verified, no matter if it is set to true or not. Skipping the verification
could lead to hard to find errors and crashes.

<a id="DEP0103"></a>
