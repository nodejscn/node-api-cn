
The HTTP/2 implementation applies stricter handling of invalid characters in
HTTP header names and values than the HTTP/1 implementation.

Header field names are *case-insensitive* and are transmitted over the wire
strictly as lower-case strings. The API provided by Node.js allows header
names to be set as mixed-case strings (e.g. `Content-Type`) but will convert
those to lower-case (e.g. `content-type`) upon transmission.

Header field-names *must only* contain one or more of the following ASCII
characters: `a`-`z`, `A`-`Z`, `0`-`9`, `!`, `#`, `$`, `%`, `&`, `'`, `*`, `+`,
`-`, `.`, `^`, `_`, `` (backtick), `|`, and `~`.

Using invalid characters within an HTTP header field name will cause the
stream to be closed with a protocol error being reported.

Header field values are handled with more leniency but *should* not contain
new-line or carriage return characters and *should* be limited to US-ASCII
characters, per the requirements of the HTTP specification.

