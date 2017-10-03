<!-- YAML
added: v8.5.0
-->

* `name` {string}
* `type` {string}
* Returns: {Array}

Returns a list of `PerformanceEntry` objects in chronological order
with respect to `performanceEntry.startTime` whose `performanceEntry.name` is
equal to `name`, and optionally, whose `performanceEntry.entryType` is equal to
`type`.

