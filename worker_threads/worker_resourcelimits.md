<!-- YAML
added:
 - v13.2.0
 - v12.16.0
-->

* {Object}
  * `maxYoungGenerationSizeMb` {number}
  * `maxOldGenerationSizeMb` {number}
  * `codeRangeSizeMb` {number}
  * `stackSizeMb` {number}

Provides the set of JS engine resource constraints inside this Worker thread.
If the `resourceLimits` option was passed to the [`Worker`][] constructor,
this matches its values.

If this is used in the main thread, its value is an empty object.

