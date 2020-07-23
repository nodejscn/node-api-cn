
Sets the max memory size of V8's old memory section. As memory
consumption approaches the limit, V8 will spend more time on
garbage collection in an effort to free unused memory.

On a machine with 2GB of memory, consider setting this to
1536 (1.5GB) to leave some memory for other uses and avoid swapping.

```console
$ node --max-old-space-size=1536 index.js
```

























