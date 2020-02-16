<!-- YAML
added: v12.16.0
-->

* {Object}
  * `maxYoungGenerationSizeMb` {number}
  * `maxOldGenerationSizeMb` {number}
  * `codeRangeSizeMb` {number}

Provides the set of JS engine resource constraints for this Worker thread.
If the `resourceLimits` option was passed to the [`Worker`][] constructor,
this matches its values.

If the worker has stopped, the return value is an empty object.
