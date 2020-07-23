
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

_defaultEnv_ is the conditional environment name priority array,
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

> 1. Let _resolvedURL_ be **undefined**.
> 1. If _specifier_ is a valid URL, then
>    1. Set _resolvedURL_ to the result of parsing and reserializing
>       _specifier_ as a URL.
> 1. Otherwise, if _specifier_ starts with _"/"_, _"./"_ or _"../"_, then
>    1. Set _resolvedURL_ to the URL resolution of _specifier_ relative to
>       _parentURL_.
> 1. Otherwise, if _specifier_ starts with _"#"_, then
>    1. Set _resolvedURL_ to the result of
>       **PACKAGE_INTERNAL_RESOLVE**(_specifier_, _parentURL_).
>    1. If _resolvedURL_ is **null** or **undefined**, throw a
>       _Package Import Not Defined_ error.
> 1. Otherwise,
>    1. Note: _specifier_ is now a bare specifier.
>    1. Set _resolvedURL_ the result of
>       **PACKAGE_RESOLVE**(_specifier_, _parentURL_).
> 1. If _resolvedURL_ contains any percent encodings of _"/"_ or _"\\"_ (_"%2f"_
>    and _"%5C"_ respectively), then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. If the file at _resolvedURL_ is a directory, then
>    1. Throw an _Unsupported Directory Import_ error.
> 1. If the file at _resolvedURL_ does not exist, then
>    1. Throw a _Module Not Found_ error.
> 1. Set _resolvedURL_ to the real path of _resolvedURL_.
> 1. Let _format_ be the result of **ESM_FORMAT**(_resolvedURL_).
> 1. Load _resolvedURL_ as module format, _format_.
> 1. Return _resolvedURL_.

**PACKAGE_RESOLVE**(_packageSpecifier_, _parentURL_)

> 1. Let _packageName_ be *undefined*.
> 1. Let _packageSubpath_ be *undefined*.
> 1. If _packageSpecifier_ is an empty string, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Otherwise,
>    1. If _packageSpecifier_ does not contain a _"/"_ separator, then
>       1. Throw an _Invalid Module Specifier_ error.
>    1. Set _packageName_ to the substring of _packageSpecifier_
>       until the second _"/"_ separator or the end of the string.
> 1. If _packageName_ starts with _"."_ or contains _"\\"_ or _"%"_, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Let _packageSubpath_ be _undefined_.
> 1. If the length of _packageSpecifier_ is greater than the length of
>    _packageName_, then
>    1. Set _packageSubpath_ to _"."_ concatenated with the substring of
>       _packageSpecifier_ from the position at the length of _packageName_.
> 1. If _packageSubpath_ contains any _"."_ or _".."_ segments or percent
>    encoded strings for _"/"_ or _"\\"_, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Let _selfUrl_ be the result of
>    **SELF_REFERENCE_RESOLVE**(_packageName_, _packageSubpath_, _parentURL_).
> 1. If _selfUrl_ isn't empty, return _selfUrl_.
> 1. If _packageSubpath_ is _undefined_ and _packageName_ is a Node.js builtin
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
>    1. If _packageSubpath_ is equal to _"./"_, then
>       1. Return _packageURL_ + _"/"_.
>    1. If _packageSubpath_ is _undefined__, then
>       1. Return the result of **PACKAGE_MAIN_RESOLVE**(_packageURL_,
>          _pjson_).
>    1. Otherwise,
>       1. If _pjson_ is not **null** and _pjson_ has an _"exports"_ key, then
>          1. Let _exports_ be _pjson.exports_.
>          1. If _exports_ is not **null** or **undefined**, then
>             1. Let _resolved_ be the result of  **PACKAGE_EXPORTS_RESOLVE**(
>                _packageURL_, _packageSubpath_, _pjson.exports_).
>             1. If _resolved_ is **null** or **undefined**, throw a
>                _Package Path Not Exported_ error.
>             1. Return _resolved_.
>       1. Return the URL resolution of _packageSubpath_ in _packageURL_.
> 1. Throw a _Module Not Found_ error.

**SELF_REFERENCE_RESOLVE**(_packageName_, _packageSubpath_, _parentURL_)

> 1. Let _packageURL_ be the result of **READ_PACKAGE_SCOPE**(_parentURL_).
> 1. If _packageURL_ is **null**, then
>    1. Return **undefined**.
> 1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
> 1. If _pjson_ does not include an _"exports"_ property, then
>    1. Return **undefined**.
> 1. If _pjson.name_ is equal to _packageName_, then
>    1. If _packageSubpath_ is equal to _"./"_, then
>       1. Return _packageURL_ + _"/"_.
>    1. If _packageSubpath_ is _undefined_, then
>       1. Return the result of **PACKAGE_MAIN_RESOLVE**(_packageURL_, _pjson_).
>    1. Otherwise,
>       1. If _pjson_ is not **null** and _pjson_ has an _"exports"_ key, then
>          1. Let _exports_ be _pjson.exports_.
>          1. If _exports_ is not **null** or **undefined**, then
>             1. Let _resolved_ be the result of **PACKAGE_EXPORTS_RESOLVE**(
>                _packageURL_, _subpath_, _pjson.exports_).
>             1. If _resolved_ is **null** or **undefined**, throw a
>                _Package Path Not Exported_ error.
>             1. Return _resolved_.
>       1. Return the URL resolution of _subpath_ in _packageURL_.
> 1. Otherwise, return **undefined**.

**PACKAGE_MAIN_RESOLVE**(_packageURL_, _pjson_)

> 1. If _pjson_ is **null**, then
>    1. Throw a _Module Not Found_ error.
> 1. If _pjson.exports_ is not **null** or **undefined**, then
>    1. If _exports_ is an Object with both a key starting with _"."_ and a key
>       not starting with _"."_, throw an _Invalid Package Configuration_ error.
>    1. If _pjson.exports_ is a String or Array, or an Object containing no
>       keys starting with _"."_, then
>       1. Let _resolved_ be the result of  **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _pjson.exports_, _""_, **false**, _defaultEnv_).
>       1. If _resolved_ is **null** or **undefined**, throw a
>          _Package Path Not Exported_ error.
>       1. Return _resolved_.
>    1. If _pjson.exports_ is an Object containing a _"."_ property, then
>       1. Let _mainExport_ be the _"."_ property in _pjson.exports_.
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _mainExport_, _""_, **false**, _defaultEnv_).
>       1. If _resolved_ is **null** or **undefined**, throw a
>          _Package Path Not Exported_ error.
>       1. Return _resolved_.
>    1. Throw a _Package Path Not Exported_ error.
> 1. Let _legacyMainURL_ be the result applying the legacy
>    **LOAD_AS_DIRECTORY** CommonJS resolver to _packageURL_, throwing a
>    _Module Not Found_ error for no resolution.
> 1. Return _legacyMainURL_.

**PACKAGE_EXPORTS_RESOLVE**(_packageURL_, _packagePath_, _exports_)
> 1. If _exports_ is an Object with both a key starting with _"."_ and a key not
>    starting with _"."_, throw an _Invalid Package Configuration_ error.
> 1. If _exports_ is an Object and all keys of _exports_ start with _"."_, then
>    1. Set _packagePath_ to _"./"_ concatenated with _packagePath_.
>    1. If _packagePath_ is a key of _exports_, then
>       1. Let _target_ be the value of _exports\[packagePath\]_.
>       1. Return **PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_,
>          _""_, **false**, _defaultEnv_).
>    1. Let _directoryKeys_ be the list of keys of _exports_ ending in
>       _"/"_, sorted by length descending.
>    1. For each key _directory_ in _directoryKeys_, do
>       1. If _packagePath_ starts with _directory_, then
>          1. Let _target_ be the value of _exports\[directory\]_.
>          1. Let _subpath_ be the substring of _target_ starting at the index
>             of the length of _directory_.
>          1. Return **PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_,
>             _subpath_, **false**, _defaultEnv_).
> 1. Return **null**.

**PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_, _subpath_, _internal_, _env_)

> 1. If _target_ is a String, then
>    1. If _target_ contains any _"node_modules"_ segments including
>       _"node_modules"_ percent-encoding, throw an _Invalid Package Target_
>       error.
>    1. If _subpath_ has non-zero length and _target_ does not end with _"/"_,
>       throw an _Invalid Module Specifier_ error.
>    1. If _target_ does not start with _"./"_, then
>       1. If _target_ does not start with _"../"_ or _"/"_ and is not a valid
>          URL, then
>          1. If _internal_ is **true**, return **PACKAGE_RESOLVE**(
>             _target_ + _subpath_, _packageURL_ + _"/"_)_.
>       1. Otherwise throw an _Invalid Package Target_ error.
>    1. Let _resolvedTarget_ be the URL resolution of the concatenation of
>       _packageURL_ and _target_.
>    1. If _resolvedTarget_ is not contained in _packageURL_, throw an
>       _Invalid Package Target_ error.
>    1. Let _resolved_ be the URL resolution of the concatenation of
>       _subpath_ and _resolvedTarget_.
>    1. If _resolved_ is not contained in _resolvedTarget_, throw an
>       _Invalid Module Specifier_ error.
>    1. Return _resolved_.
> 1. Otherwise, if _target_ is a non-null Object, then
>    1. If _exports_ contains any index property keys, as defined in ECMA-262
>       [6.1.7 Array Index][], throw an _Invalid Package Configuration_ error.
>    1. For each property _p_ of _target_, in object insertion order as,
>       1. If _p_ equals _"default"_ or _env_ contains an entry for _p_, then
>          1. Let _targetValue_ be the value of the _p_ property in _target_.
>          1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>             _packageURL_, _targetValue_, _subpath_, _internal_, _env_)
>          1. If _resolved_ is equal to **undefined**, continue the loop.
>          1. Return _resolved_.
>    1. Return **undefined**.
> 1. Otherwise, if _target_ is an Array, then
>    1. If _target.length is zero, return **null**.
>    1. For each item _targetValue_ in _target_, do
>       1. Let _resolved_ be the result of **PACKAGE_TARGET_RESOLVE**(
>          _packageURL_, _targetValue_, _subpath_, _internal_, _env_),
>          continuing the loop on any _Invalid Package Target_ error.
>       1. If _resolved_ is **undefined**, continue the loop.
>       1. Return _resolved_.
>    1. Return or throw the last fallback resolution **null** return or error.
> 1. Otherwise, if _target_ is _null_, return **null**.
> 1. Otherwise throw an _Invalid Package Target_ error.

**PACKAGE_INTERNAL_RESOLVE**(_specifier_, _parentURL_)

> 1. Assert: _specifier_ begins with _"#"_.
> 1. If _specifier_ is exactly equal to _"#"_ or starts with _"#/"_, then
>    1. Throw an _Invalid Module Specifier_ error.
> 1. Let _packageURL_ be the result of **READ_PACKAGE_SCOPE**(_parentURL_).
> 1. If _packageURL_ is not **null**, then
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_packageURL_).
>    1. If _pjson.imports is a non-null Object, then
>       1. Let _imports_ be _pjson.imports_.
>       1. If _specifier_ is a key of _imports_, then
>          1. Let _target_ be the value of _imports\[specifier\]_.
>          1. Return **PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_,
>             _""_, **true**, _defaultEnv_).
>       1. Let _directoryKeys_ be the list of keys of _imports_ ending in
>          _"/"_, sorted by length descending.
>       1. For each key _directory_ in _directoryKeys_, do
>          1. If _specifier_ starts with _directory_, then
>             1. Let _target_ be the value of _imports\[directory\]_.
>             1. Let _subpath_ be the substring of _target_ starting at the
>                index of the length of _directory_.
>             1. Return **PACKAGE_TARGET_RESOLVE**(_packageURL_, _target_,
>                _subpath_, **true**, _defaultEnv_).
> 1. Return **null**.

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
>    1. If _scopeURL_ ends in a _"node_modules"_ path segment, return **null**.
>    1. Let _pjson_ be the result of **READ_PACKAGE_JSON**(_scopeURL_).
>    1. If _pjson_ is not **null**, then
>       1. Return _pjson_.
>    1. Set _scopeURL_ to the parent URL of _scopeURL_.
> 1. Return **null**.

**READ_PACKAGE_JSON**(_packageURL_)

> 1. Let _pjsonURL_ be the resolution of _"package.json"_ within _packageURL_.
> 1. If the file at _pjsonURL_ does not exist, then
>    1. Return **null**.
> 1. If the file at _packageURL_ does not parse as valid JSON, then
>    1. Throw an _Invalid Package Configuration_ error.
> 1. Return the parsed JSON source of the file at _pjsonURL_.

</details>

