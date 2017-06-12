
The `type` is a string that represents the type of resource that caused
`init` to call. Generally it will be the name of the resource's constructor.
The resource types provided by the built-in Node.js modules are:

```
FSEVENTWRAP, FSREQWRAP, GETADDRINFOREQWRAP, GETNAMEINFOREQWRAP, HTTPPARSER,
JSSTREAM, PIPECONNECTWRAP, PIPEWRAP, PROCESSWRAP, QUERYWRAP, SHUTDOWNWRAP,
SIGNALWRAP, STATWATCHER, TCPCONNECTWRAP, TCPWRAP, TIMERWRAP, TTYWRAP,
UDPSENDWRAP, UDPWRAP, WRITEWRAP, ZLIB, SSLCONNECTION, PBKDF2REQUEST,
RANDOMBYTESREQUEST, TLSWRAP
```

Users are be able to define their own `type` when using the public embedder API.

*Note:* It is possible to have type name collisions. Embedders are encouraged
to use a unique prefixes, such as the npm package name, to prevent collisions
when listening to the hooks.

