
* {string}

The `subprocess.spawnfile` property indicates the executable file name of
the child process that is launched.

For [`child_process.fork()`][], its value will be equal to
[`process.execPath`][].
For [`child_process.spawn()`][], its value will be the name of
the executable file.
For [`child_process.exec()`][],  its value will be the name of the shell
in which the child process is launched.

