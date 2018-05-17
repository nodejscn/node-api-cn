
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

[`AHAFS`]: https://www.ibm.com/developerworks/aix/library/au-aix_event_infrastructure/
[`Buffer.byteLength`]: buffer.html#buffer_class_method_buffer_bytelength_string_encoding
[`Buffer`]: buffer.html#buffer_buffer
[`FSEvents`]: https://developer.apple.com/library/mac/documentation/Darwin/Conceptual/FSEvents_ProgGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005289-CH1-SW1
[`ReadDirectoryChangesW`]: https://msdn.microsoft.com/en-us/library/windows/desktop/aa365465%28v=vs.85%29.aspx
[`ReadStream`]: #fs_class_fs_readstream
[`URL`]: url.html#url_the_whatwg_url_api
[`UV_THREADPOOL_SIZE`]: cli.html#cli_uv_threadpool_size_size
[`WriteStream`]: #fs_class_fs_writestream
[`EventEmitter`]: events.html
[`event ports`]: http://illumos.org/man/port_create
[`fs.FSWatcher`]: #fs_class_fs_fswatcher
[`fs.Stats`]: #fs_class_fs_stats
[`fs.access()`]: #fs_fs_access_path_mode_callback
[`fs.chmod()`]: #fs_fs_chmod_path_mode_callback
[`fs.chown()`]: #fs_fs_chown_path_uid_gid_callback
[`fs.copyFile()`]: #fs_fs_copyfile_src_dest_flags_callback
[`fs.exists()`]: fs.html#fs_fs_exists_path_callback
[`fs.fstat()`]: #fs_fs_fstat_fd_callback
[`fs.futimes()`]: #fs_fs_futimes_fd_atime_mtime_callback
[`fs.lstat()`]: #fs_fs_lstat_path_callback
[`fs.mkdir()`]: #fs_fs_mkdir_path_mode_callback
[`fs.mkdtemp()`]: #fs_fs_mkdtemp_prefix_options_callback
[`fs.open()`]: #fs_fs_open_path_flags_mode_callback
[`fs.read()`]: #fs_fs_read_fd_buffer_offset_length_position_callback
[`fs.readFile()`]: #fs_fs_readfile_path_options_callback
[`fs.readFileSync()`]: #fs_fs_readfilesync_path_options
[`fs.rmdir()`]: #fs_fs_rmdir_path_callback
[`fs.stat()`]: #fs_fs_stat_path_callback
[`fs.utimes()`]: #fs_fs_utimes_path_atime_mtime_callback
[`fs.watch()`]: #fs_fs_watch_filename_options_listener
[`fs.write()`]: #fs_fs_write_fd_buffer_offset_length_position_callback
[`fs.writeFile()`]: #fs_fs_writefile_file_data_options_callback
[`inotify`]: http://man7.org/linux/man-pages/man7/inotify.7.html
[`kqueue`]: https://www.freebsd.org/cgi/man.cgi?kqueue
[`net.Socket`]: net.html#net_class_net_socket
[`stat()`]: fs.html#fs_fs_stat_path_callback
[`util.promisify()`]: util.html#util_util_promisify_original
[Caveats]: #fs_caveats
[Common System Errors]: errors.html#errors_common_system_errors
[FS Constants]: #fs_fs_constants_1
[MDN-Date]: https://developer.mozilla.org/en-US/JavaScript/Reference/Global_Objects/Date
[MDN-Number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type
[MSDN-Rel-Path]: https://msdn.microsoft.com/en-us/library/windows/desktop/aa365247.aspx#fully_qualified_vs._relative_paths
[Readable Streams]: stream.html#stream_class_stream_readable
[Writable Stream]: stream.html#stream_class_stream_writable
[inode]: https://en.wikipedia.org/wiki/Inode
[Naming Files, Paths, and Namespaces]: https://msdn.microsoft.com/en-us/library/windows/desktop/aa365247(v=vs.85).aspx
[MSDN-Using-Streams]: https://msdn.microsoft.com/en-us/library/windows/desktop/bb540537.aspx
[support of file system `flags`]: #fs_file_system_flags
