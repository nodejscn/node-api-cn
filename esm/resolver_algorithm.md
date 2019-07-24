
The algorithm to load an ES module specifier is given through the
**ESM_RESOLVE** method below. It returns the resolved URL for a
module specifier relative to a parentURL, in addition to the unique module
format for that resolved URL given by the **ESM_FORMAT** routine.

The _"module"_ format is returned for an ECMAScript Module, while the
_"commonjs"_ format is used to indicate loading through the legacy
CommonJS loader. Additional formats such as _"addon"_ can be extended in future
updates.

In the following algorithms, all subroutine errors are propagated as errors
of these top-level routines.

_isMain_ is **true** when resolving the Node.js application entry point.

<details>
<summary>Resolver algorithm specification</summary>

**ESM_RESOLVE(_specifier_, _parentURL_, _isMain_)**
> 1. Let _resolvedURL_ be **undefined**.
> 1. If _specifier_ is a valid URL, then
>    1. Set _resolvedURL_ to the result of parsing and reserializing
>       _specifier_ as a URL.
> 1. Otherwise, if _specifier_ starts with _"/"_, then
>    1. Throw an _Invalid Specifier_ error.
> 1. Otherwise, if _specifier_ starts with _"./"_ or _"../"_, then
>    1. Set _resolvedURL_ to the URL resolution of _specifier_ relative to
>       _parentURL_.
> 1. Otherwise,
>    1. Note: _specifier_ is now a bare specifier.
>    1. Set _resolvedURL_ the result of
>       **PACKAGE_RESOLVE**(_specifier_, _parentURL_).
> 1. If the file at _resolvedURL_ does not exist, then
>    1. Throw a _Module Not Found_ error.
> 1. Set _resolvedURL_ to the real path of _resolvedURL_.
> 1. Let _format_ be the result of **ESM_FORMAT**(_resolvedURL_, _isMain_).
> 1. Load _resolvedURL_ as module format, _format_.

PACKAGE_RESOLVE(_packageSpecifier_, _parentURL_)
> 1. Let _packageName_ be *undefined*.
> 1. Let _packageSubpath_ be *undefined*.
> 1. If _packageSpecifier_ is an empty string, then
>    1. Throw an _Invalid Specifier_ error.
> 1. If _packageSpecifier_ does not start with _"@"_, then
>    1. Set _packageName_ to the substring of _packageSpecifier_ until the
>       first _"/"_ separator or the end of the string.
> 1. Otherwise,
>    1. If _packageSpecifier_ does not contain a _"/"_ separator, then
>       1. Throw an _Invalid Specifier_ error.
>    1. Set _packageName_ to the substring of _packageSpecifier_
>       until the second _"/"_ separator or the end of the string.
> 1. Let _packageSubpath_ be the substring of _packageSpecifier_ from the
>    position at the length of _packageName_ plus one, if any.
> 1. Assert: _packageName_ is a valid package name or scoped package name.
> 1. Assert: _packageSubpath_ is either empty, or a path without a leading
>    separator.
> 1. If _packageSubpath_ contains any _"."_ or _".."_ segments or percent
>    encoded strings for _"/"_ or _"\\"_ then,
>    1. Throw an _Invalid Specifier_ error.
> 1. If _packageSubpath_ is empty and _packageName_ is a Node.js builtin
>    module, then
>    1. Return the string _"node:"_ concatenated with _packageSpecifier_.
> 1. While _parentURL_ is not the file system root,
>    1. Let _packageURL_ be the URL resolution of "node_modules/"
>       concatenated with _packageSpecifier_, relative to _parentURL_.
>    1. Set _parentURL_ to the parent folder URL of _parentURL_.
>    1. If the folder at _packageURL_ does not exist, then
>       1. Set _parentURL_ to the parent URL path of _parentURL_.
>       1. Continue the next loop iteration.
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
>    1. If _packageSubpath_ is empty, then
>       1. Return the result of **PACKAGE_MAIN_RESOLVE**(_packageURL_,
>          _pjson_).
>    1. Otherwise,
>       1. Return the URL resolution of _packageSubpath_ in _packageURL_.
> 1. Throw a _Module Not Found_ error.

PACKAGE_MAIN_RESOLVE(_packageURL_, _pjson_)
> 1. If _pjson_ is **null**, then
>    1. Throw a _Module Not Found_ error.
> 1. If _pjson.main_ is a String, then
>    1. Let _resolvedMain_ be the concatenation of _packageURL_, "/", and
>       _pjson.main_.
>    1. If the file at _resolvedMain_ exists, then
>       1. Return _resolvedMain_.
> 1. If _pjson.type_ is equal to _"module"_, then
>    1. Throw a _Module Not Found_ error.
> 1. Let _legacyMainURL_ be the result applying the legacy
>    **LOAD_AS_DIRECTORY** CommonJS resolver to _packageURL_, throwing a
>    _Module Not Found_ error for no resolution.
> 1. If _legacyMainURL_ does not end in _".js"_ then,
>    1. Throw an _Unsupported File Extension_ error.
> 1. Return _legacyMainURL_.

**ESM_FORMAT(_url_, _isMain_)**
> 1. Assert: _url_ corresponds to an existing file.
> 1. Let _pjson_ be the result of **READ_PACKAGE_SCOPE**(_url_).
> 1. If _url_ ends in _".mjs"_, then
>    1. Return _"module"_.
> 1. If _url_ ends in _".cjs"_, then
>    1. Return _"commonjs"_.
> 1. If _pjson?.type_ exists and is _"module"_, then
>    1. If _isMain_ is **true** or _url_ ends in _".js"_, then
>       1. Return _"module"_.
>    1. Throw an _Unsupported File Extension_ error.
> 1. Otherwise,
>    1. If _isMain_ is **true** or _url_ ends in _".js"_, _".json"_ or
>       _".node"_, then
>       1. Return _"commonjs"_.
>    1. Throw an _Unsupported File Extension_ error.

READ_PACKAGE_SCOPE(_url_)
> 1. Let _scopeURL_ be _url_.
> 1. While _scopeURL_ is not the file system root,
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_scopeURL_).
>    1. If _pjson_ is not **null**, then
>       1. Return _pjson_.
>    1. Set _scopeURL_ to the parent URL of _scopeURL_.
> 1. Return **null**.

READ_PACKAGE_JSON(_packageURL_)
> 1. Let _pjsonURL_ be the resolution of _"package.json"_ within _packageURL_.
> 1. If the file at _pjsonURL_ does not exist, then
>    1. Return **null**.
> 1. If the file at _packageURL_ does not parse as valid JSON, then
>    1. Throw an _Invalid Package Configuration_ error.
> 1. Return the parsed JSON source of the file at _pjsonURL_.

</details>

