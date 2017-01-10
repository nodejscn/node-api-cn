<!-- YAML
added: v0.11.4
-->

* `options` {Object} A set of options providing information for name generation
  * `host` {String} A domain name or IP address of the server to issue the request to
  * `port` {Number} Port of remote server
  * `localAddress` {String} Local interface to bind for network connections
    when issuing the request
* Returns: {String}

Get a unique name for a set of request options, to determine whether a
connection can be reused.  In the http agent, this returns
`host:port:localAddress`.  In the https agent, the name includes the
CA, cert, ciphers, and other HTTPS/TLS-specific options that determine
socket reusability.

