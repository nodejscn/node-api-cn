
System calls like open(2) and read(2) define the interface between user programs
and the underlying operating system. Node functions which simply wrap a syscall,
like `fs.open()`, will document that. The docs link to the corresponding man
pages (short for manual pages) which describe how the syscalls work.

**Caveat:** some syscalls, like lchown(2), are BSD-specific. That means, for
example, that `fs.lchown()` only works on Mac OS X and other BSD-derived systems,
and is not available on Linux.

Most Unix syscalls have Windows equivalents, but behavior may differ on Windows
relative to Linux and OS X. For an example of the subtle ways in which it's
sometimes impossible to replace Unix syscall semantics on Windows, see [Node
issue 4760](https://github.com/nodejs/node/issues/4760).

[submit an issue]: https://github.com/nodejs/node/issues/new
[the contributing guide]: https://github.com/nodejs/node/blob/master/CONTRIBUTING.md
