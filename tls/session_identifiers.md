
Servers generate a unique ID for new connections and
send it to the client. Clients and servers save the session state. When
reconnecting, clients send the ID of their saved session state and if the server
also has the state for that ID, it can agree to use it. Otherwise, the server
will create a new session. See [RFC 2246][] for more information, page 23 and
30.

Resumption using session identifiers is supported by most web browsers when
making HTTPS requests.

For Node.js, clients wait for the [`'session'`][] event to get the session data,
and provide the data to the `session` option of a subsequent [`tls.connect()`][]
to reuse the session. Servers must
implement handlers for the [`'newSession'`][] and [`'resumeSession'`][] events
to save and restore the session data using the session ID as the lookup key to
reuse sessions. To reuse sessions across load balancers or cluster workers,
servers must use a shared session cache (such as Redis) in their session
handlers.

