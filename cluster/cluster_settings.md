<!-- YAML
added: v0.7.1
-->

* {Object}
  * `execArgv` {Array} list of string arguments passed to the Node.js
    executable. (Default=`process.execArgv`)
  * `exec` {String} file path to worker file.  (Default=`process.argv[1]`)
  * `args` {Array} string arguments passed to worker.
    (Default=`process.argv.slice(2)`)
  * `silent` {Boolean} whether or not to send output to parent's stdio.
    (Default=`false`)
  * `stdio` {Array} Configures the stdio of forked processes. Because the
    cluster module relies on IPC to function, this configuration must contain an
    `'ipc'` entry. When this option is provided, it overrides `silent`.
  * `uid` {Number} Sets the user identity of the process. (See setuid(2).)
  * `gid` {Number} Sets the group identity of the process. (See setgid(2).)

After calling `.setupMaster()` (or `.fork()`) this settings object will contain
the settings, including the default values.

This object is not supposed to be changed or set manually, by you.

