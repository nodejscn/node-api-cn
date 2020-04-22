
<!--introduced_in=v8.2.0-->
<!-- type=misc -->

Node.js has many features that make it easier to write internationalized
programs. Some of them are:

* Locale-sensitive or Unicode-aware functions in the [ECMAScript Language
  Specification][ECMA-262]:
  * [`String.prototype.normalize()`][]
  * [`String.prototype.toLowerCase()`][]
  * [`String.prototype.toUpperCase()`][]
* All functionality described in the [ECMAScript Internationalization API
  Specification][ECMA-402] (aka ECMA-402):
  * [`Intl`][] object
  * Locale-sensitive methods like [`String.prototype.localeCompare()`][] and
    [`Date.prototype.toLocaleString()`][]
* The [WHATWG URL parser][]'s [internationalized domain names][] (IDNs) support
* [`require('buffer').transcode()`][]
* More accurate [REPL][] line editing
* [`require('util').TextDecoder`][]
* [`RegExp` Unicode Property Escapes][]

Node.js (and its underlying V8 engine) uses [ICU][] to implement these features
in native C/C++ code. The full ICU data set is provided by Node.js by default.
However, due to the size of the ICU data file, several
options are provided for customizing the ICU data set either when
building or running Node.js.

