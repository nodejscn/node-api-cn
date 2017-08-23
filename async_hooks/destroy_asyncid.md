
* `asyncId` {number}

Called after the resource corresponding to `asyncId` is destroyed. It is also called
asynchronously from the embedder API `emitDestroy()`.

*Note:* Some resources depend on GC for cleanup, so if a reference is made to
the `resource` object passed to `init` it's possible that `destroy` is
never called, causing a memory leak in the application. Of course if
the resource doesn't depend on GC then this isn't an issue.

