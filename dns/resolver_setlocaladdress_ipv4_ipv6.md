<!-- YAML
added: v15.1.0
-->

* `ipv4` {string} A string representation of an IPv4 address.
  **Default:** `'0.0.0.0'`
* `ipv6` {string} A string representation of an IPv6 address.
  **Default:** `'::0'`

The resolver instance will send its requests from the specified IP address.
This allows programs to specify outbound interfaces when used on multi-homed
systems.

If a v4 or v6 address is not specified, it is set to the default, and the
operating system will choose a local address automatically.

The resolver will use the v4 local address when making requests to IPv4 DNS
servers, and the v6 local address when making requests to IPv6 DNS servers.
The `rrtype` of resolution requests has no impact on the local address used.

