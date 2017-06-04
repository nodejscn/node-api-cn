<!-- YAML
added: v0.1.28
-->

* Returns: {integer}

The `process.getuid()` method returns the numeric user identity of the process.
(See getuid(2).)

```js
if (process.getuid) {
  console.log(`Current uid: ${process.getuid()}`);
}
```

*Note*: This function is only available on POSIX platforms (i.e. not Windows
or Android).

