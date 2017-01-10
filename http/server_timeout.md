<!-- YAML
added: v0.9.12
-->

* {Number} Default = 120000 (2 minutes)

The number of milliseconds of inactivity before a socket is presumed
to have timed out.

Note that the socket timeout logic is set up on connection, so
changing this value only affects *new* connections to the server, not
any existing connections.

Set to 0 to disable any kind of automatic timeout behavior on incoming
connections.

