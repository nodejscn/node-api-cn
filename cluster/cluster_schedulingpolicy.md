<!-- YAML
added: v0.11.2
-->


调度策略，包括循环计数的 `cluster.SCHED_RR`，以及由操作系统决定的`cluster.SCHED_NONE`。
这是一个全局设置，当第一个工作进程被衍生或者调动`cluster.setupMaster()`时，都将第一时间生效。

除Windows外的所有操作系统中，`SCHED_RR`都是默认设置。只要libuv可以有效地分发IOCP handle，而不会导致严重的性能冲击的话，Windows系统也会更改为`SCHED_RR`。

`cluster.schedulingPolicy` 可以通过设置`NODE_CLUSTER_SCHED_POLICY`环境变量来实现。这个环境变量的有效值包括`"rr"` 和 `"none"`。

