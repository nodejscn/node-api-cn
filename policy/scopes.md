
Use the `"scopes"` field of a manifest to set configuration for many resources
at once. The `"scopes"` field works by matching resources by their segments.
If a scope or resource includes `"cascade": true`, unknown specifiers will
be searched for in their containing scope. The containing scope for cascading
is found by recursively reducing the resource URL by removing segments for
[special schemes][], keeping trailing `"/"` suffixes, and removing the query and
hash fragment. This leads to the eventual reduction of the URL to its origin.
If the URL is non-special the scope will be located by the URL's origin. If no
scope is found for the origin or in the case of opaque origins, a protocol
string can be used as a scope.

Note, `blob:` URLs adopt their origin from the path they contain, and so a scope
of `"blob:https://nodejs.org"` will have no effect since no URL can have an
origin of `blob:https://nodejs.org`; URLs starting with
`blob:https://nodejs.org/` will use `https://nodejs.org` for its origin and
thus `https:` for its protocol scope. For opaque origin `blob:` URLs they will
have `blob:` for their protocol scope since they do not adopt origins.

