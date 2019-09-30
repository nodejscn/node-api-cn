<!-- YAML
added: v12.6.0
-->

* Returns: {Object} the resource usage for the current process. All of these
  values come from the `uv_getrusage` call which returns
  a [`uv_rusage_t` struct][uv_rusage_t].
  * `userCPUTime` {integer} maps to `ru_utime` computed in microseconds.
    It is the same value as [`process.cpuUsage().user`][process.cpuUsage].
  * `systemCPUTime` {integer} maps to `ru_stime` computed in microseconds.
    It is the same value as [`process.cpuUsage().system`][process.cpuUsage].
  * `maxRSS` {integer} maps to `ru_maxrss` which is the maximum resident set
    size used in kilobytes.
  * `sharedMemorySize` {integer} maps to `ru_ixrss` but is not supported by
    any platform.
  * `unsharedDataSize` {integer} maps to `ru_idrss` but is not supported by
    any platform.
  * `unsharedStackSize` {integer} maps to `ru_isrss` but is not supported by
    any platform.
  * `minorPageFault` {integer} maps to `ru_minflt` which is the number of
    minor page faults for the process, see
    [this article for more details][wikipedia_minor_fault].
  * `majorPageFault` {integer} maps to `ru_majflt` which is the number of
    major page faults for the process, see
    [this article for more details][wikipedia_major_fault]. This field is not
    supported on Windows.
  * `swappedOut` {integer} maps to `ru_nswap` but is not supported by any
    platform.
  * `fsRead` {integer} maps to `ru_inblock` which is the number of times the
    file system had to perform input.
  * `fsWrite` {integer} maps to `ru_oublock` which is the number of times the
    file system had to perform output.
  * `ipcSent` {integer} maps to `ru_msgsnd` but is not supported by any
    platform.
  * `ipcReceived` {integer} maps to `ru_msgrcv` but is not supported by any
    platform.
  * `signalsCount` {integer} maps to `ru_nsignals` but is not supported by any
    platform.
  * `voluntaryContextSwitches` {integer} maps to `ru_nvcsw` which is the
    number of times a CPU context switch resulted due to a process voluntarily
    giving up the processor before its time slice was completed (usually to
    await availability of a resource). This field is not supported on Windows.
  * `involuntaryContextSwitches` {integer} maps to `ru_nivcsw` which is the
    number of times a CPU context switch resulted due to a higher priority
    process becoming runnable or because the current process exceeded its
    time slice. This field is not supported on Windows.

```js
console.log(process.resourceUsage());
/*
  Will output:
  {
    userCPUTime: 82872,
    systemCPUTime: 4143,
    maxRSS: 33164,
    sharedMemorySize: 0,
    unsharedDataSize: 0,
    unsharedStackSize: 0,
    minorPageFault: 2469,
    majorPageFault: 0,
    swappedOut: 0,
    fsRead: 0,
    fsWrite: 8,
    ipcSent: 0,
    ipcReceived: 0,
    signalsCount: 0,
    voluntaryContextSwitches: 79,
    involuntaryContextSwitches: 1
  }
*/
```

