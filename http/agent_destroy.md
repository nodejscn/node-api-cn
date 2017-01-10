<!-- YAML
added: v0.11.4
-->

Destroy any sockets that are currently in use by the agent.

It is usually not necessary to do this.  However, if you are using an
agent with KeepAlive enabled, then it is best to explicitly shut down
the agent when you know that it will no longer be used.  Otherwise,
sockets may hang open for quite a long time before the server
terminates them.

