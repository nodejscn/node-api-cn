<!-- YAML
added: v0.9.4
-->

* `groups` {Array}

The `process.setgroups()` method sets the supplementary group IDs for the
Node.js process. This is a privileged operation that requires the Node.js process
to have `root` or the `CAP_SETGID` capability.

The `groups` array can contain numeric group IDs, group names or both.

*Note*: This function is only available on POSIX platforms (i.e. not Windows
or Android).

