<!-- YAML
added: v12.15.0
-->

Use an insecure HTTP parser that accepts invalid HTTP headers. This may allow
interoperability with non-conformant HTTP implementations. It may also allow
request smuggling and other HTTP attacks that rely on invalid headers being
accepted. Avoid using this option.

