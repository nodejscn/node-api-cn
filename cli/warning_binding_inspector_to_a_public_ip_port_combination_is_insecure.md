
Binding the inspector to a public IP (including `0.0.0.0`) with an open port is
insecure, as it allows external hosts to connect to the inspector and perform
a [remote code execution][] attack.

If you specify a host, make sure that at least one of the following is true:
either the host is not public, or the port is properly firewalled to disallow
unwanted connections.

**More specifically, `--inspect=0.0.0.0` is insecure if the port (`9229` by
default) is not firewall-protected.**

See the [debugging security implications][] section for more information.

