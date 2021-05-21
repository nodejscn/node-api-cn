
<!-- YAML
added:
  - v15.1.0
  - v12.22.0
-->

The `v8.stopCoverage()` method allows the user to stop the coverage collection
started by [`NODE_V8_COVERAGE`][], so that V8 can release the execution count
records and optimize code. This can be used in conjunction with
[`v8.takeCoverage()`][] if the user wants to collect the coverage on demand.

