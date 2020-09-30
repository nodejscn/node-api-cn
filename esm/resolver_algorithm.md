
The algorithm to load an ES module specifier is given through the
**ESM_RESOLVE** method below. It returns the resolved URL for a
module specifier relative to a parentURL.

The algorithm to determine the module format of a resolved URL is
provided by **ESM_FORMAT**, which returns the unique module
format for any file. The _"module"_ format is returned for an ECMAScript
Module, while the _"commonjs"_ format is used to indicate loading through the
legacy CommonJS loader. Additional formats such as _"addon"_ can be extended in
future updates.

In the following algorithms, all subroutine errors are propagated as errors
of these top-level routines unless stated otherwise.

_defaultConditions_ is the conditional environment name array,
`["node", "import"]`.

The resolver can throw the following errors:
* _Invalid Module Specifier_: Module specifier is an invalid URL, package name
  or package subpath specifier.
* _Invalid Package Configuration_: package.json configuration is invalid or
  contains an invalid configuration.
* _Invalid Package Target_: Package exports or imports define a target module
  for the package that is an invalid type or string target.
* _Package Path Not Exported_: Package exports do not define or permit a target
  subpath in the package for the given module.
* _Package Import Not Defined_: Package imports do not define the specifier.
* _Module Not Found_: The package or module requested does not exist.

<details>
<summary>Resolver algorithm specification</summary>

**ESM_RESOLVE**(_specifier_, _parentURL_)

> 1. Let _resolved_ be **undefined**.
> 1. If _specifier_ is a valid URL, then
>    1. Set _resolved_ to the result of parsing and reserializing
>       _specifier_ as a URL.
> 1. Otherwise, if _specifier_ starts with _"/"_, _"./"_ or _"../"_, then
>    1. Set _resolved_ to the URL resolution of _specifier_ relative to
>       _parentURL_.
> 1. Otherwise, if _specifier_ starts with _"#"_, then
>    1. Set _resolved_ to the destructured value of the result of
>       **PACKAGE_IMPORTS_RESOLVE**(_specifier_, _parentURL_,
>       _defaultConditions_).
> 1. Otherwise,
>    1. Note: _specifier_ is now a bare specifier.
>    1. Set _resolved_ the result of
>       **PACKAGE_RESOLVE**(_specifier_, _parentURL_).
> 1. If _resolved_ contains any percent encodings of _"/"_ or _"\\"_ (_"%2f"_
>    and _"%5C"_ respectively), then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. If the file at _resolved_ is a directory, then
>    1. Throw an _Unsupported Directory Import_ error.
> 1. If the file at _resolved_ does not exist, then
>    1. Throw a _Module Not Found_ error.
> 1. Set _resolved_ to the real path of _resolved_.
> 1. Let _format_ be the result of **ESM_FORMAT**(_resolved_).
> 1. Load _resolved_ as module format, _format_.
> 1. Return _resolved_.

**PACKAGE_RESOLVE**(_packageSpecifier_, _parentURL_)

> 1. Let _packageName_ be **undefined**.
> 1. If _packageSpecifier_ is an empty string, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. If _packageSpecifier_ does not start with _"@"_, then
>    1. Set _packageName_ to the substring of _packageSpecifier_ until the first
>       _"/"_ separator or the end of the string.
> 1. Otherwise,
>    1. If _packageSpecifier_ does not contain a _"/"_ separator, then
>       1. Throw an _Invalid Module Specifier_ error.
>    1. Set _packageName_ to the substring of _packageSpecifier_
>       until the second _"/"_ separator or the end of the string.
> 1. If _packageName_ starts with _"."_ or contains _"\\"_ or _"%"_, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Let _packageSubpath_ be _"."_ concatenated with the substring of
>       _packageSpecifier_ from the position at the length of _packageName_.
> 1. Let _selfUrl_ be the result of
>    **PACKAGE_SELF_RESOLVE**(_packageName_, _packageSubpath_, _parentURL_).
> 1. If _selfUrl_ is not **undefined**, return _selfUrl_.
> 1. If _packageSubpath_ is _"."_ and _packageName_ is a Node.js builtin
>    module, then
>    1. Return the string _"nodejs:"_ concatenated with _packageSpecifier_.
> 1. While _parentURL_ is not the file system root,
>    1. Let _packageURL_ be the URL resolution of _"node_modules/"_
>       concatenated with _packageSpecifier_, relative to _parentURL_.
>    1. Set _parentURL_ to the parent folder URL of _parentURL_.
>    1. If the folder at _packageURL_ does not exist, then
>       1. Set _parentURL_ to the parent URL path of _parentURL_.
>       1. Continue the next loop iteration.
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
>    1. If _pjson_ is not **null** and _pjson_._exports_ is not **null** or
>       **undefined**, then
>       1. Let _exports_ be _pjson.exports_.
>       1. Return the _resolved_ destructured value of the result of
>          **PACKAGE_EXPORTS_RESOLVE**(_packageURL_, _packageSubpath_,
>           _pjson.exports_, _defaultConditions_).
>    1. Otherwise, if _packageSubpath_ is equal to _"."_, then
>       1. Return the result applying the legacy **LOAD_AS_DIRECTORY**
>          CommonJS resolver to _packageURL_, throwing a _Module Not Found_
>          error for no resolution.
>    1. Otherwise,
>       1. Return the URL resolution of _packageSubpath_ in _packageURL_.
> 1. Throw a _Module Not Found_ error.

**PACKAGE_SELF_RESOLVE**(_packageName_, _packageSubpath_, _parentURL_)

> 1. Let _packageURL_ be the result of **READ_PACKAGE_SCOPE**(_parentURL_).
> 1. If _packageURL_ is **null**, then
>    1. Return **undefined**.
> 1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
> 1. If _pjson_ is **null** or if _pjson_._exports_ is **null** or
>    **undefined**, then
>    1. Return **undefined**.
> 1. If _pjson.name_ is equal to _packageName_, then
>    1. Return the _resolved_ destructured value of the result of
>       **PACKAGE_EXPORTS_RESOLVE**(_packageURL_, _subpath_, _pjson.exports_,
>       _defaultConditions_).
> 1. Otherwise, return **undefined**.

**PACKAGE_EXPORTS_RESOLVE**(_packageURL_, _subpath_, _exports_, _conditions_)

> 1. If _exports_ is an Object with both a key starting with _"."_ and a key not
>    starting with _"."_, throw an _Invalid Package Configuration_ error.
> 1. If _subpath_ is equal to _"."_, then
>    1. Let _mainExport_ be **undefined**.
>    1. If _exports_ is a String or Array, or an Object containing no keys
>       starting with _"."_, then
>       1. Set _mainExport_ to _exports_.
>    1. Otherwise if _exports_ is an Object containing a _"."_ property, then
>       1. Set _mainExport_ to _exports_\[_"."_\].
>    1. If _mainExport_ is not **undefined**, then
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _mainExport_, _""_, **false**, **false**,
>          _conditions_).
>       1. If _resolved_ is not **null** or **undefined**, then
>          1. Return _resolved_.
> 1. Otherwise, if _exports_ is an Object and all keys of _exports_ start with
>    _"."_, then
>    1. Let _matchKey_ be the string _"./"_ concatenated with _subpath_.
>    1. Let _resolvedMatch_ be result of **PACKAGE_IMPORTS_EXPORTS_RESOLVE**(
>       _matchKey_, _exports_, _packageURL_, **false**, _conditions_).
>    1. If _resolvedMatch_._resolve_ is not **null** or **undefined**, then
>       1. Return _resolvedMatch_.
> 1. Throw a _Package Path Not Exported_ error.

**PACKAGE_IMPORTS_RESOLVE**(_specifier_, _parentURL_, _conditions_)

> 1. Assert: _specifier_ begins with _"#"_.
> 1. If _specifier_ is exactly equal to _"#"_ or starts with _"#/"_, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Let _packageURL_ be the result of **READ_PACKAGE_SCOPE**(_parentURL_).
> 1. If _packageURL_ is not **null**, then
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
>    1. If _pjson.imports_ is a non-null Object, then
>       1. Let _resolvedMatch_ be the result of
>          **PACKAGE_IMPORTS_EXPORTS_RESOLVE**(_specifier_, _pjson.imports_,
>          _packageURL_, **true**, _conditions_).
>       1. If _resolvedMatch_._resolve_ is not **null** or **undefined**, then
>          1. Return _resolvedMatch_.
> 1. Throw a _Package Import Not Defined_ error.

**PACKAGE_IMPORTS_EXPORTS_RESOLVE**(_matchKey_, _matchObj_, _packageURL_,
_isImports_, _conditions_)

> 1. If _matchKey_ is a key of _matchObj_, and does not end in _"*"_, then
>    1. Let _target_ be the value of _matchObj_\[_matchKey_\].
>    1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>       _packageURL_, _target_, _""_, **false**, _isImports_, _conditions_).
>    1. Return the object _{ resolved, exact: **true** }_.
> 1. Let _expansionKeys_ be the list of keys of _matchObj_ ending in _"/"_
>    or _"*"_, sorted by length descending.
> 1. For each key _expansionKey_ in _expansionKeys_, do
>    1. If _expansionKey_ ends in _"*"_ and _matchKey_ starts with but is
>       not equal to the substring of _expansionKey_ excluding the last _"*"_
>       character, then
>       1. Let _target_ be the value of _matchObj_\[_expansionKey_\].
>       1. Let _subpath_ be the substring of _matchKey_ starting at the
>          index of the length of _expansionKey_ minus one.
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _target_, _subpath_, **true**, _isImports_,
>          _conditions_).
>       1. Return the object _{ resolved, exact: **true** }_.
>    1. If _matchKey_ starts with _expansionKey_, then
>       1. Let _target_ be the value of _matchObj_\[_expansionKey_\].
>       1. Let _subpath_ be the substring of _matchKey_ starting at the
>          index of the length of _expansionKey_.
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _target_, _subpath_, **false**, _isImports_,
>          _conditions_).
>       1. Return the object _{ resolved, exact: **false** }_.
> 1. Return the object _{ resolved: **null**, exact: **true** }_.

**PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_, _subpath_, _pattern_,
_internal_, _conditions_)

> 1. If _target_ is a String, then
>    1. If _pattern_ is **false**, _subpath_ has non-zero length and _target_
>       does not end with _"/"_, throw an _Invalid Module Specifier_ error.
>    1. If _target_ does not start with _"./"_, then
>       1. If _internal_ is **true** and _target_ does not start with _"../"_ or
>          _"/"_ and is not a valid URL, then
>          1. If _pattern_ is **true**, then
>             1. Return **PACKAGE_RESOLVE**(_target_ with every instance of
>                _"*"_ replaced by _subpath_, _packageURL_ + _"/"_)_.
>          1. Return **PACKAGE_RESOLVE**(_target_ + _subpath_,
>             _packageURL_ + _"/"_)_.
>       1. Otherwise, throw an _Invalid Package Target_ error.
>    1. If _target_ split on _"/"_ or _"\\"_ contains any _"."_, _".."_ or
>       _"node_modules"_ segments after the first segment, throw an
>       _Invalid Package Target_ error.
>    1. Let _resolvedTarget_ be the URL resolution of the concatenation of
>       _packageURL_ and _target_.
>    1. Assert: _resolvedTarget_ is contained in _packageURL_.
>    1. If _subpath_ split on _"/"_ or _"\\"_ contains any _"."_, _".."_ or
>       _"node_modules"_ segments, throw an _Invalid Module Specifier_ error.
>    1. If _pattern_ is **true**, then
>       1. Return the URL resolution of _resolvedTarget_ with every instance of
>          _"*"_ replaced with _subpath_.
>    1. Otherwise,
>       1. Return the URL resolution of the concatenation of _subpath_ and
>          _resolvedTarget_.
> 1. Otherwise, if _target_ is a non-null Object, then
>    1. If _exports_ contains any index property keys, as defined in ECMA-262
>       [6.1.7 Array Index][], throw an _Invalid Package Configuration_ error.
>    1. For each property _p_ of _target_, in object insertion order as,
>       1. If _p_ equals _"default"_ or _conditions_ contains an entry for _p_,
>          then
>          1. Let _targetValue_ be the value of the _p_ property in _target_.
>          1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>             _packageURL_, _targetValue_, _subpath_, _pattern_, _internal_,
>             _conditions_).
>          1. If _resolved_ is equal to **undefined**, continue the loop.
>          1. Return _resolved_.
>    1. Return **undefined**.
> 1. Otherwise, if _target_ is an Array, then
>    1. If _target.length is zero, return **null**.
>    1. For each item _targetValue_ in _target_, do
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _targetValue_, _subpath_, _pattern_, _internal_,
>          _conditions_), continuing the loop on any _Invalid Package Target_
>          error.
>       1. If _resolved_ is **undefined**, continue the loop.
>       1. Return _resolved_.
>    1. Return or throw the last fallback resolution **null** return or error.
> 1. Otherwise, if _target_ is _null_, return **null**.
> 1. Otherwise throw an _Invalid Package Target_ error.

**ESM_FORMAT**(_url_)

> 1. Assert: _url_ corresponds to an existing file.
> 1. Let _pjson_ be the result of **READ_PACKAGE_SCOPE**(_url_).
> 1. If _url_ ends in _".mjs"_, then
>    1. Return _"module"_.
> 1. If _url_ ends in _".cjs"_, then
>    1. Return _"commonjs"_.
> 1. If _pjson?.type_ exists and is _"module"_, then
>    1. If _url_ ends in _".js"_, then
>       1. Return _"module"_.
>    1. Throw an _Unsupported File Extension_ error.
> 1. Otherwise,
>    1. Throw an _Unsupported File Extension_ error.

**READ_PACKAGE_SCOPE**(_url_)

> 1. Let _scopeURL_ be _url_.
> 1. While _scopeURL_ is not the file system root,
>    1. Set _scopeURL_ to the parent URL of _scopeURL_.
>    1. If _scopeURL_ ends in a _"node_modules"_ path segment, return **null**.
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_scopeURL_).
>    1. If _pjson_ is not **null**, then
>       1. Return _pjson_.
> 1. Return **null**.

**READ_PACKAGE_JSON**(_packageURL_)

> 1. Let _pjsonURL_ be the resolution of _"package.json"_ within _packageURL_.
> 1. If the file at _pjsonURL_ does not exist, then
>    1. Return **null**.
> 1. If the file at _packageURL_ does not parse as valid JSON, then
>    1. Throw an _Invalid Package Configuration_ error.
> 1. Return the parsed JSON source of the file at _pjsonURL_.

</details>

