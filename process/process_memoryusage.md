<!-- YAML
added: v0.1.16
-->

* Returns: {Object}
    * `rss` {Integer}
    * `heapTotal` {Integer}
    * `heapUsed` {Integer}
    * `external` {Integer}

The `process.memoryUsage()` method returns an object describing the memory usage
of the Node.js process measured in bytes.

For example, the code:

```js
console.log(process.memoryUsage());
```

Will generate:

```js
{
  rss: 4935680,
  heapTotal: 1826816,
  heapUsed: 650472,
  external: 49879
}
```

`heapTotal` and `heapUsed` refer to V8's memory usage.
`external` refers to the memory usage of C++ objects bound to JavaScript
objects managed by V8.

