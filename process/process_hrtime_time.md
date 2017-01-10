<!-- YAML
added: v0.7.6
-->

The `process.hrtime()` method returns the current high-resolution real time in a
`[seconds, nanoseconds]` tuple Array. `time` is an optional parameter that must
be the result of a previous `process.hrtime()` call (and therefore, a real time
in a `[seconds, nanoseconds]` tuple Array containing a previous time) to diff
with the current time. These times are relative to an arbitrary time in the
past, and not related to the time of day and therefore not subject to clock
drift. The primary use is for measuring performance between intervals.

Passing in the result of a previous call to `process.hrtime()` is useful for
calculating an amount of time passed between calls:

```js
var time = process.hrtime();
// [ 1800216, 25 ]

setTimeout(() => {
  var diff = process.hrtime(time);
  // [ 1, 552 ]

  console.log(`Benchmark took ${diff[0] * 1e9 + diff[1]} nanoseconds`);
  // benchmark took 1000000527 nanoseconds
}, 1000);
```

Constructing an array by some method other than calling `process.hrtime()` and
passing the result to process.hrtime() will result in undefined behavior.


