
The following flags are available wherever the `flag` option takes a
string:

* `'a'` - Open file for appending.
  The file is created if it does not exist.

* `'ax'` - Like `'a'` but fails if the path exists.

* `'a+'` - Open file for reading and appending.
  The file is created if it does not exist.

* `'ax+'` - Like `'a+'` but fails if the path exists.

* `'as'` - Open file for appending in synchronous mode.
  The file is created if it does not exist.

* `'as+'` - Open file for reading and appending in synchronous mode.
  The file is created if it does not exist.

* `'r'` - Open file for reading.
  An exception occurs if the file does not exist.

* `'r+'` - Open file for reading and writing.
  An exception occurs if the file does not exist.

* `'rs+'` - Open file for reading and writing in synchronous mode. Instructs
  the operating system to bypass the local file system cache.

  This is primarily useful for opening files on NFS mounts as it allows
  skipping the potentially stale local cache. It has a very real impact on
  I/O performance so using this flag is not recommended unless it is needed.

  Note that this doesn't turn `fs.open()` or `fsPromises.open()` into a
  synchronous blocking call. If synchronous operation is desired, something
  like `fs.openSync()` should be used.

* `'w'` - Open file for writing.
  The file is created (if it does not exist) or truncated (if it exists).

* `'wx'` - Like `'w'` but fails if the path exists.

* `'w+'` - Open file for reading and writing.
The file is created (if it does not exist) or truncated (if it exists).

* `'wx+'` - Like `'w+'` but fails if the path exists.

`flag` can also be a number as documented by open(2); commonly used constants
are available from `fs.constants`. On Windows, flags are translated to
their equivalent ones where applicable, e.g. `O_WRONLY` to `FILE_GENERIC_WRITE`,
or `O_EXCL|O_CREAT` to `CREATE_NEW`, as accepted by `CreateFileW`.

The exclusive flag `'x'` (`O_EXCL` flag in open(2)) ensures that path is newly
created. On POSIX systems, path is considered to exist even if it is a symlink
to a non-existent file. The exclusive flag may or may not work with network
file systems.

On Linux, positional writes don't work when the file is opened in append mode.
The kernel ignores the position argument and always appends the data to
the end of the file.

Modifying a file rather than replacing it may require a flags mode of `'r+'`
rather than the default mode `'w'`.

The behavior of some flags are platform-specific. As such, opening a directory
on macOS and Linux with the `'a+'` flag - see example below - will return an
error. In contrast, on Windows and FreeBSD, a file descriptor or a `FileHandle`
will be returned.

```js
// macOS and Linux
fs.open('<directory>', 'a+', (err, fd) => {
  // => [Error: EISDIR: illegal operation on a directory, open <directory>]
});

// Windows and FreeBSD
fs.open('<directory>', 'a+', (err, fd) => {
  // => null, <fd>
});
```

On Windows, opening an existing hidden file using the `'w'` flag (either
through `fs.open()` or `fs.writeFile()` or `fsPromises.open()`) will fail with
`EPERM`. Existing hidden files can be opened for writing with the `'r+'` flag.

A call to `fs.ftruncate()` or `fsPromises.ftruncate()` can be used to reset
the file contents.

