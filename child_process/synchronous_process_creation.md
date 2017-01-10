
The [`child_process.spawnSync()`][], [`child_process.execSync()`][], and
[`child_process.execFileSync()`][] methods are **synchronous** and **WILL** block
the Node.js event loop, pausing execution of any additional code until the
spawned process exits.

Blocking calls like these are mostly useful for simplifying general purpose
scripting tasks and for simplifying the loading/processing of application
configuration at startup.

