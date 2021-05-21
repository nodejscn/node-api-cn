<!-- YAML
added: v15.6.0
-->

When using `--secure-heap`, the `--secure-heap-min` flag specifies the
minimum allocation from the secure heap. The minimum value is `2`.
The maximum value is the lesser of `--secure-heap` or `2147483647`.
The value given must be a power of two.

