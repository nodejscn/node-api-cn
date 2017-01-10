<!-- YAML
added: v0.1.27
-->

Uses the DNS protocol to resolve a hostname (e.g. `'nodejs.org'`) into an
array of the record types specified by `rrtype`.

Valid values for `rrtype` are:

 * `'A'` - IPV4 addresses, default
 * `'AAAA'` - IPV6 addresses
 * `'MX'` - mail exchange records
 * `'TXT'` - text records
 * `'SRV'` - SRV records
 * `'PTR'` - PTR records
 * `'NS'` - name server records
 * `'CNAME'` - canonical name records
 * `'SOA'` - start of authority record
 * `'NAPTR'` - name authority pointer record

The `callback` function has arguments `(err, addresses)`. When successful,
`addresses` will be an array, except when resolving an SOA record which returns
an object structured in the same manner as one returned by the
[`dns.resolveSoa()`][] method. The type of each item in `addresses` is
determined by the record type, and described in the documentation for the
corresponding lookup methods.

On error, `err` is an [`Error`][] object, where `err.code` is
one of the error codes listed [here](#dns_error_codes).

