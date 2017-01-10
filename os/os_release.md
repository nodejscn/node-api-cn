<!-- YAML
added: v0.3.3
-->

* Returns: {String}

The `os.release()` method returns a string identifying the operating system
release.

*Note*: On POSIX systems, the operating system release is determined by calling
uname(3). On Windows, `GetVersionExW()` is used. Please see
https://en.wikipedia.org/wiki/Uname#Examples for more information.

