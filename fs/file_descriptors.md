
On POSIX systems, for every process, the kernel maintains a table of currently
open files and resources. Each open file is assigned a simple numeric
identifier called a *file descriptor*. At the system-level, all file system
operations use these file descriptors to identify and track each specific
file. Windows systems use a different but conceptually similar mechanism for
tracking resources. To simplify things for users, Node.js abstracts away the
specific differences between operating systems and assigns all open files a
numeric file descriptor.

The `fs.open()` method is used to allocate a new file descriptor. Once
allocated, the file descriptor may be used to read data from, write data to,
or request information about the file.

```js
fs.open('/open/some/file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.fstat(fd, (err, stat) => {
    if (err) throw err;
    // use stat

    // always close the file descriptor!
    fs.close(fd, (err) => {
      if (err) throw err;
    });
  });
});
```

Most operating systems limit the number of file descriptors that may be open
at any given time so it is critical to close the descriptor when operations
are completed. Failure to do so will result in a memory leak that will
eventually cause an application to crash.

