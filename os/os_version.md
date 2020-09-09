<!-- YAML
added: v13.11.0
-->

* Returns {string}

Returns a string identifying the kernel version.

On POSIX systems, the operating system release is determined by calling
[`uname(3)`][]. On Windows, `RtlGetVersion()` is used, and if it is not
available, `GetVersionExW()` will be used. See
<https://en.wikipedia.org/wiki/Uname#Examples> for more information.

