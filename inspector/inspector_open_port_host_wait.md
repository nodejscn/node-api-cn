
* port {number} Port to listen on for inspector connections. Optional,
  defaults to what was specified on the CLI.
* host {string} Host to listen on for inspector connections. Optional,
  defaults to what was specified on the CLI.
* wait {boolean} Block until a client has connected. Optional, defaults
  to false.

Activate inspector on host and port. Equivalent to `node
--inspect=[[host:]port]`, but can be done programatically after node has
started.

If wait is `true`, will block until a client has connected to the inspect port
and flow control has been passed to the debugger client.

