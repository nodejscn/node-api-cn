<!-- YAML
added: v14.3.0
-->

Print short summaries of calls to [`Atomics.wait()`][] to stderr.
The output could look like this:

```text
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 0, 1, inf) started
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 0, 1, inf) did not wait because the values mismatched
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 0, 0, 10) started
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 0, 0, 10) timed out
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 4, 0, inf) started
(node:15701) [Thread 1] Atomics.wait(&lt;address> + 4, -1, inf) started
(node:15701) [Thread 0] Atomics.wait(&lt;address> + 4, 0, inf) was woken up by another thread
(node:15701) [Thread 1] Atomics.wait(&lt;address> + 4, -1, inf) was woken up by another thread
```

The fields here correspond to:

* The thread id as given by [`worker_threads.threadId`][]
* The base address of the `SharedArrayBuffer` in question, as well as the
  byte offset corresponding to the index passed to `Atomics.wait()`
* The expected value that was passed to `Atomics.wait()`
* The timeout passed to `Atomics.wait`

