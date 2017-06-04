
These functions are implemented quite differently than [`dns.lookup()`][]. They
do not use getaddrinfo(3) and they _always_ perform a DNS query on the
network. This network communication is always done asynchronously, and does not
use libuv's threadpool.

As a result, these functions cannot have the same negative impact on other
processing that happens on libuv's threadpool that [`dns.lookup()`][] can have.

They do not use the same set of configuration files than what [`dns.lookup()`][]
uses. For instance, _they do not use the configuration from `/etc/hosts`_.

[`Error`]: errors.html#errors_class_error
[`dns.lookup()`]: #dns_dns_lookup_hostname_options_callback
[`dns.resolve4()`]: #dns_dns_resolve4_hostname_options_callback
[`dns.resolve6()`]: #dns_dns_resolve6_hostname_options_callback
[`dns.resolveCname()`]: #dns_dns_resolvecname_hostname_callback
[`dns.resolveMx()`]: #dns_dns_resolvemx_hostname_callback
[`dns.resolveNaptr()`]: #dns_dns_resolvenaptr_hostname_callback
[`dns.resolveNs()`]: #dns_dns_resolvens_hostname_callback
[`dns.resolvePtr()`]: #dns_dns_resolveptr_hostname_callback
[`dns.resolveSoa()`]: #dns_dns_resolvesoa_hostname_callback
[`dns.resolveSrv()`]: #dns_dns_resolvesrv_hostname_callback
[`dns.resolveTxt()`]: #dns_dns_resolvetxt_hostname_callback
[DNS error codes]: #dns_error_codes
[Implementation considerations section]: #dns_implementation_considerations
[supported `getaddrinfo` flags]: #dns_supported_getaddrinfo_flags
[the official libuv documentation]: http://docs.libuv.org/en/latest/threadpool.html
[`util.promisify()`]: util.html#util_util_promisify_original
