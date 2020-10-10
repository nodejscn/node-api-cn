
The servers encrypt the entire session state and send it
to the client as a "ticket". When reconnecting, the state is sent to the server
in the initial connection. This mechanism avoids the need for server-side
session cache. If the server doesn't use the ticket, for any reason (failure
to decrypt it, it's too old, etc.), it will create a new session and send a new
ticket. See [RFC 5077][] for more information.
服务器加密整个会话状态，并将其发送给客户端，被称为“票据（ticket）”。当需要复用会话时，客户端
在握手阶段将ticket发送给服务器。这种机制的优点是服务器端不需要缓存会话状态。如果基于任何
原因（包括解密ticket内容失败，ticket信息超时等情况），服务器不使用ticket，则会新建一个会话，并
发送新的ticket给客户端，详见[RFC 5077][]。

Resumption using session tickets is becoming commonly supported by many web
browsers when making HTTPS requests.
基于tickets的会话复用方式正在被越来越多的主流浏览器支持。

For Node.js, clients use the same APIs for resumption with session identifiers
as for resumption with session tickets. For debugging, if
[`tls.TLSSocket.getTLSTicket()`][] returns a value, the session data contains a
ticket, otherwise it contains client-side session state.
在Node.js中，客户端的两种会话复用使用相同的API。在调试时，如果[`tls.TLSSocket.getTLSTicket()`][]
返回了会话信息，并且会话信息中包含ticket，则使用了Session Ticket会话复用，
否则使用了Session ID会话复用。

With TLSv1.3, be aware that multiple tickets may be sent by the server,
resulting in multiple `'session'` events, see [`'session'`][] for more
information.
在TLS1.3中，需要注意服务器可能会发送多个ticket，这会触发多个`'session'`事件，详见[`'session'`][]
事件中的介绍。

Single process servers need no specific implementation to use session tickets.
To use session tickets across server restarts or load balancers, servers must
all have the same ticket keys. There are three 16-byte keys internally, but the
tls API exposes them as a single 48-byte buffer for convenience.
单个服务器使用session ticket会话复用不需要特别的实现，但如果需要在服务器重启后或者在使用
负载均衡的情况下，任然能够复用成功，则所有服务器必须要使用相同的密钥来生成ticket。这个密钥
由三个16字节的密钥组成，但在API实现中，为了方便使用了一个48字节的缓存保存。

Its possible to get the ticket keys by calling [`server.getTicketKeys()`][] on
one server instance and then distribute them, but it is more reasonable to
securely generate 48 bytes of secure random data and set them with the
`ticketKeys` option of [`tls.createServer()`][]. The keys should be regularly
regenerated and server's keys can be reset with
[`server.setTicketKeys()`][].


Session ticket keys are cryptographic keys, and they ***must be stored
securely***. With TLS 1.2 and below, if they are compromised all sessions that
used tickets encrypted with them can be decrypted. They should not be stored
on disk, and they should be regenerated regularly.

If clients advertise support for tickets, the server will send them. The
server can disable tickets by supplying
`require('constants').SSL_OP_NO_TICKET` in `secureOptions`.

Both session identifiers and session tickets timeout, causing the server to
create new sessions. The timeout can be configured with the `sessionTimeout`
option of [`tls.createServer()`][].

For all the mechanisms, when resumption fails, servers will create new sessions.
Since failing to resume the session does not cause TLS/HTTPS connection
failures, it is easy to not notice unnecessarily poor TLS performance. The
OpenSSL CLI can be used to verify that servers are resuming sessions. Use the
`-reconnect` option to `openssl s_client`, for example:

```console
$ openssl s_client -connect localhost:443 -reconnect
```

Read through the debug output. The first connection should say "New", for
example:

```text
New, TLSv1.2, Cipher is ECDHE-RSA-AES128-GCM-SHA256
```

Subsequent connections should say "Reused", for example:

```text
Reused, TLSv1.2, Cipher is ECDHE-RSA-AES128-GCM-SHA256
```

