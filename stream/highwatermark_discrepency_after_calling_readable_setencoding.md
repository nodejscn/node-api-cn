
The use of `readable.setEncoding()` will change the behavior of how the
`highWaterMark` operates in non-object mode.

Typically, the size of the current buffer is measured against the
`highWaterMark` in _bytes_. However, after `setEncoding()` is called, the
comparison function will begin to measure the buffer's size in _characters_.

This is not a problem in common cases with `latin1` or `ascii`. But it is
advised to be mindful about this behavior when working with strings that could
contain multi-byte characters.
