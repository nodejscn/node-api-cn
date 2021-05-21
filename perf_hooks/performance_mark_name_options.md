<!-- YAML
added: v8.5.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37136
    description: Updated to conform to the User Timing Level 3 specification.
-->

* `name` {string}
* `options` {Object}
  * `detail` {any} Additional optional detail to include with the mark.
  * `startTime` {number} An optional timestamp to be used as the mark time.
    **Defaults**: `performance.now()`.

Creates a new `PerformanceMark` entry in the Performance Timeline. A
`PerformanceMark` is a subclass of `PerformanceEntry` whose
`performanceEntry.entryType` is always `'mark'`, and whose
`performanceEntry.duration` is always `0`. Performance marks are used
to mark specific significant moments in the Performance Timeline.

