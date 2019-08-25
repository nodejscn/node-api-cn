<!-- YAML
added: v0.8.4
-->

* `hostname` {string} The host name or IP address to verify the certificate
  against.
* `cert` {Object} A [certificate object][] representing the peer's certificate.
* Returns: {Error|undefined}

Verifies the certificate `cert` is issued to `hostname`.

Returns {Error} object, populating it with `reason`, `host`, and `cert` on
failure. On success, returns {undefined}.

This function can be overwritten by providing alternative function as part of
the `options.checkServerIdentity` option passed to `tls.connect()`. The
overwriting function can call `tls.checkServerIdentity()` of course, to augment
the checks done with additional verification.

This function is only called if the certificate passed all other checks, such as
being issued by trusted CA (`options.ca`).

