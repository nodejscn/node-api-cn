<!-- YAML
added: v15.6.0
-->

* Returns: {integer}

The `process.memoryUsage.rss()` method returns an integer representing the
Resident Set Size (RSS) in bytes.

The Resident Set Size, is the amount of space occupied in the main
memory device (that is a subset of the total allocated memory) for the
process, including all C++ and JavaScript objects and code.

This is the same value as the `rss` property provided by `process.memoryUsage()`
but `process.memoryUsage.rss()` is faster.

```js
console.log(process.memoryUsage.rss());
// 35655680
```

