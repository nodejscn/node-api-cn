<!-- YAML
added: v0.1.28
-->

The `process.setuid(id)` method sets the user identity of the process. (See
setuid(2).)  The `id` can be passed as either a numeric ID or a username string.
If a username is specified, the method blocks while resolving the associated
numeric ID.

```js
if (process.getuid && process.setuid) {
  console.log(`Current uid: ${process.getuid()}`);
  try {
    process.setuid(501);
    console.log(`New uid: ${process.getuid()}`);
  } catch (err) {
    console.log(`Failed to set uid: ${err}`);
  }
}
```

*Note*: This function is only available on POSIX platforms (i.e. not Windows
or Android).


