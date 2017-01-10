<!-- YAML
added: v6.0.0
-->

`fs` functions support passing and receiving paths as both strings
and Buffers. The latter is intended to make it possible to work with
filesystems that allow for non-UTF-8 filenames. For most typical
uses, working with paths as Buffers will be unnecessary, as the string
API converts to and from UTF-8 automatically.

*Note* that on certain file systems (such as NTFS and HFS+) filenames
will always be encoded as UTF-8. On such file systems, passing
non-UTF-8 encoded Buffers to `fs` functions will not work as expected.

