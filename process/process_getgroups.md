<!-- YAML
added: v0.9.4
-->

* Returns: {Array}

The `process.getgroups()` method returns an array with the supplementary group
IDs. POSIX leaves it unspecified if the effective group ID is included but
Node.js ensures it always is.

*Note*: This function is only available on POSIX platforms (i.e. not Windows
or Android).

