
When set, Node.js will begin outputting [V8 JavaScript code coverage][] to the
directory provided as an argument. Coverage is output as an array of


```json
{
  "result": [
    {
      "scriptId": "67",
      "url": "internal/tty.js",
      "functions": []
    }
  ]
}
```

`NODE_V8_COVERAGE` will automatically propagate to subprocesses, making it
easier to instrument applications that call the `child_process.spawn()` family
of functions. `NODE_V8_COVERAGE` can be set to an empty string, to prevent
propagation.

At this time coverage is only collected in the main thread and will not be
output for code executed by worker threads.

