<!-- YAML
added: v15.1.0
-->

> Stability: 1 - Experimental

Writes a V8 heap snapshot to disk when the V8 heap usage is approaching the
heap limit. `count` should be a non-negative integer (in which case
Node.js will write no more than `max_count` snapshots to disk).

When generating snapshots, garbage collection may be triggered and bring
the heap usage down, therefore multiple snapshots may be written to disk
before the Node.js instance finally runs out of memory. These heap snapshots
can be compared to determine what objects are being allocated during the
time consecutive snapshots are taken. It's not guaranteed that Node.js will
write exactly `max_count` snapshots to disk, but it will try
its best to generate at least one and up to `max_count` snapshots before the
Node.js instance runs out of memory when `max_count` is greater than `0`.

Generating V8 snapshots takes time and memory (both memory managed by the
V8 heap and native memory outside the V8 heap). The bigger the heap is,
the more resources it needs. Node.js will adjust the V8 heap to accommodate
the additional V8 heap memory overhead, and try its best to avoid using up
all the memory available to the process. When the process uses
more memory than the system deems appropriate, the process may be terminated
abruptly by the system, depending on the system configuration.

```console
$ node --max-old-space-size=100 --heapsnapshot-near-heap-limit=3 index.js
Wrote snapshot to Heap.20200430.100036.49580.0.001.heapsnapshot
Wrote snapshot to Heap.20200430.100037.49580.0.002.heapsnapshot
Wrote snapshot to Heap.20200430.100038.49580.0.003.heapsnapshot

<--- Last few GCs --->

[49580:0x110000000]     4826 ms: Mark-sweep 130.6 (147.8) -> 130.5 (147.8) MB, 27.4 / 0.0 ms  (average mu = 0.126, current mu = 0.034) allocation failure scavenge might not succeed
[49580:0x110000000]     4845 ms: Mark-sweep 130.6 (147.8) -> 130.6 (147.8) MB, 18.8 / 0.0 ms  (average mu = 0.088, current mu = 0.031) allocation failure scavenge might not succeed


<--- JS stacktrace --->

FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory
....
```

