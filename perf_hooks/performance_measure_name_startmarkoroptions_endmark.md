<!-- YAML
added: v8.5.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37136
    description: Updated to conform to the User Timing Level 3 specification.
  - version:
      - v13.13.0
      - v12.16.3
    pr-url: https://github.com/nodejs/node/pull/32651
    description: Make `startMark` and `endMark` parameters optional.
-->

* `name` {string}
* `startMarkOrOptions` {string|Object} Optional.
  * `detail` {any} Additional optional detail to include with the measure.
  * `duration` {number} Duration between start and end times.
  * `end` {number|string} Timestamp to be used as the end time, or a string
    identifying a previously recorded mark.
  * `start` {number|string} Timestamp to be used as the start time, or a string
    identifying a previously recorded mark.
* `endMark` {string} Optional. Must be omitted if `startMarkOrOptions` is an
  {Object}.

Creates a new `PerformanceMeasure` entry in the Performance Timeline. A
`PerformanceMeasure` is a subclass of `PerformanceEntry` whose
`performanceEntry.entryType` is always `'measure'`, and whose
`performanceEntry.duration` measures the number of milliseconds elapsed since
`startMark` and `endMark`.

The `startMark` argument may identify any *existing* `PerformanceMark` in the
Performance Timeline, or *may* identify any of the timestamp properties
provided by the `PerformanceNodeTiming` class. If the named `startMark` does
not exist, an error is thrown.

The optional `endMark` argument must identify any *existing* `PerformanceMark`
in the Performance Timeline or any of the timestamp properties provided by the
`PerformanceNodeTiming` class. `endMark` will be `performance.now()`
if no parameter is passed, otherwise if the named `endMark` does not exist, an
error will be thrown.

