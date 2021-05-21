<!-- YAML
added: v15.6.0
-->

* Returns: {Object}
  * `total` {number} The total allocated secure heap size as specified
    using the `--secure-heap=n` command-line flag.
  * `min` {number} The minimum allocation from the secure heap as
    specified using the `--secure-heap-min` command-line flag.
  * `used` {number} The total number of bytes currently allocated from
    the secure heap.
  * `utilization` {number} The calculated ratio of `used` to `total`
    allocated bytes.

