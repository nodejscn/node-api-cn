<!-- YAML
added:
 - v13.6.0
 - v12.17.0
-->

Re-map the Node.js static code to large memory pages at startup. If supported on
the target system, this will cause the Node.js static code to be moved onto 2
MiB pages instead of 4 KiB pages.

The following values are valid for `mode`:
* `off`: No mapping will be attempted. This is the default.
* `on`: If supported by the OS, mapping will be attempted. Failure to map will
  be ignored and a message will be printed to standard error.
* `silent`: If supported by the OS, mapping will be attempted. Failure to map
  will be ignored and will not be reported.

