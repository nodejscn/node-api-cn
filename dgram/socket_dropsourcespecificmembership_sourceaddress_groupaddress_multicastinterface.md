<!-- YAML
added:
 - v13.1.0
 - v12.16.0
-->

* `sourceAddress` {string}
* `groupAddress` {string}
* `multicastInterface` {string}

Instructs the kernel to leave a source-specific multicast channel at the given
`sourceAddress` and `groupAddress` using the `IP_DROP_SOURCE_MEMBERSHIP`
socket option. This method is automatically called by the kernel when the
socket is closed or the process terminates, so most apps will never have
reason to call this.

If `multicastInterface` is not specified, the operating system will attempt to
drop membership on all valid interfaces.

