
Under the hood, [`dns.lookup()`][] uses the same operating system facilities
as most other programs. For instance, [`dns.lookup()`][] will almost always
resolve a given name the same way as the `ping` command. On most POSIX-like
operating systems, the behavior of the [`dns.lookup()`][] function can be
modified by changing settings in nsswitch.conf(5) and/or resolv.conf(5),
but note that changing these files will change the behavior of _all other
programs running on the same operating system_.

Though the call to `dns.lookup()` will be asynchronous from JavaScript's
perspective, it is implemented as a synchronous call to getaddrinfo(3) that
runs on libuv's threadpool. Because libuv's threadpool has a fixed size, it
means that if for whatever reason the call to getaddrinfo(3) takes a long
time, other operations that could run on libuv's threadpool (such as filesystem
operations) will experience degraded performance. In order to mitigate this
issue, one potential solution is to increase the size of libuv's threadpool by
setting the `'UV_THREADPOOL_SIZE'` environment variable to a value greater than
`4` (its current default value). For more information on libuv's threadpool, see
[the official libuv documentation][].

