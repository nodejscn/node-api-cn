<!-- YAML
added: v12.4.0
-->

> Stability: 1 - Experimental

Starts the V8 heap profiler on start up, and writes the heap profile to disk
before exit.

If `--heap-prof-dir` is not specified, the generated profile will be placed
in the current working directory.

If `--heap-prof-name` is not specified, the generated profile will be
named `Heap.${yyyymmdd}.${hhmmss}.${pid}.${tid}.${seq}.heapprofile`.

```console
$ node --heap-prof index.js
$ ls *.heapprofile
Heap.20190409.202950.15293.0.001.heapprofile
```

