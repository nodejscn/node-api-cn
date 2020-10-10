
The servers encrypt the entire session state and send it
to the client as a "ticket". When reconnecting, the state is sent to the server
in the initial connection. This mechanism avoids the need for server-side
session cache. If the server doesn't use the ticket, for any reason (failure
to decrypt it, it's too old, etc.), it will create a new session and send a new
ticket. See [RFC 5077][] for more information.

Resumption using session tickets is becoming commonly supported by many web
browsers when making HTTPS requests.

For Node.js, clients use the same APIs for resumption with session identifiers
as for resumption with session tickets. For debugging, if
[`tls.TLSSocket.getTLSTicket()`][] returns a value, the session data contains a
ticket, otherwise it contains client-side session state.

With TLSv1.3, be aware that multiple tickets may be sent by the server,
resulting in multiple `'session'` events, see [`'session'`][] for more
information.

Single process servers need no specific implementation to use session tickets.
To use session tickets across server restarts or load balancers, servers must
all have the same ticket keys. There are three 16-byte keys internally, but the
tls API exposes them as a single 48-byte buffer for convenience.

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

