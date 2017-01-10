
An alternative way of enabling and accessing the debugger is to start
Node.js with the `--debug` command-line flag or by signaling an existing
Node.js process with `SIGUSR1`.

Once a process has been set in debug mode this way, it can be inspected
using the Node.js debugger by either connecting to the `pid` of the running
process or via URI reference to the listening debugger:

* `node debug -p <pid>` - Connects to the process via the `pid`
* `node debug <URI>` - Connects to the process via the URI such as
localhost:5858

