
The `type` is a string that represents the type of resource that caused
`init` to be called. Generally, it will correspond to the name of the
resource's constructor.

```text
FSEVENTWRAP, FSREQWRAP, GETADDRINFOREQWRAP, GETNAMEINFOREQWRAP, HTTPPARSER,
JSSTREAM, PIPECONNECTWRAP, PIPEWRAP, PROCESSWRAP, QUERYWRAP, SHUTDOWNWRAP,
SIGNALWRAP, STATWATCHER, TCPCONNECTWRAP, TCPWRAP, TIMERWRAP, TTYWRAP,
UDPSENDWRAP, UDPWRAP, WRITEWRAP, ZLIB, SSLCONNECTION, PBKDF2REQUEST,
RANDOMBYTESREQUEST, TLSWRAP, Timeout, Immediate, TickObject
```

There is also the `PROMISE` resource type, which is used to track `Promise`
instances and asynchronous work scheduled by them.

Users are be able to define their own `type` when using the public embedder API.

*Note:* It is possible to have type name collisions. Embedders are encouraged
to use a unique prefixes, such as the npm package name, to prevent collisions
when listening to the hooks.

