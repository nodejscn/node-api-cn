<!-- YAML
added: v0.9.4
-->

* `groups` {integer[]}

The `process.setgroups()` method sets the supplementary group IDs for the
Node.js process. This is a privileged operation that requires the Node.js
process to have `root` or the `CAP_SETGID` capability.

The `groups` array can contain numeric group IDs, group names, or both.

```js
if (process.getgroups && process.setgroups) {
  try {
    process.setgroups([501]);
    console.log(process.getgroups()); // new groups
  } catch (err) {
    console.log(`Failed to set groups: ${err}`);
  }
}
```

This function is only available on POSIX platforms (i.e. not Windows or
Android).
This feature is not available in [`Worker`][] threads.

