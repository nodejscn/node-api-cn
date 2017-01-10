<!-- YAML
added: v0.3.3
-->

* Returns: {Array}

The `os.loadavg()` method returns an array containing the 1, 5, and 15 minute
load averages.

The load average is a measure of system activity, calculated by the operating
system and expressed as a fractional number.  As a rule of thumb, the load
average should ideally be less than the number of logical CPUs in the system.

The load average is a UNIX-specific concept with no real equivalent on
Windows platforms. On Windows, the return value is always `[0, 0, 0]`.

