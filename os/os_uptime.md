<!-- YAML
added: v0.3.3
-->

* Returns: {Integer}

The `os.uptime()` method returns the system uptime in number of seconds.

*Note*: Within Node.js' internals, this number is represented as a `double`.
However, fractional seconds are not returned and the value can typically be
treated as an integer.

