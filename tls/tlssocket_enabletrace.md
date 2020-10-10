<!-- YAML
added: v12.2.0
-->

When enabled, TLS packet trace information is written to `stderr`. This can be
used to debug TLS connection problems.

Note: The format of the output is identical to the output of `openssl s_client
-trace` or `openssl s_server -trace`. While it is produced by OpenSSL's
`SSL_trace()` function, the format is undocumented, can change without notice,
and should not be relied on.

