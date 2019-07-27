<!-- YAML
added: v12.0.0
-->

> Stability: 1 - Experimental

Starts the V8 CPU profiler on start up, and writes the CPU profile to disk
before exit.

If `--cpu-prof-dir` is not specified, the generated profile will be placed
in the current working directory.

If `--cpu-prof-name` is not specified, the generated profile will be
named `CPU.${yyyymmdd}.${hhmmss}.${pid}.${tid}.${seq}.cpuprofile`.

```console
$ node --cpu-prof index.js
$ ls *.cpuprofile
CPU.20190409.202950.15293.0.0.cpuprofile
```

