<!-- YAML
added: v0.5.10
-->

* `filename` {String | Buffer}
* `options` {String | Object}
  * `persistent` {Boolean} Indicates whether the process should continue to run
    as long as files are being watched. default = `true`
  * `recursive` {Boolean} Indicates whether all subdirectories should be
    watched, or only the current directory. The applies when a directory is
    specified, and only on supported platforms (See [Caveats][]). default =
    `false`
  * `encoding` {String} Specifies the character encoding to be used for the
     filename passed to the listener. default = `'utf8'`
* `listener` {Function}

Watch for changes on `filename`, where `filename` is either a file or a
directory.  The returned object is a [`fs.FSWatcher`][].

The second argument is optional. If `options` is provided as a string, it
specifies the `encoding`. Otherwise `options` should be passed as an object.

The listener callback gets two arguments `(eventType, filename)`.  `eventType` is either
`'rename'` or `'change'`, and `filename` is the name of the file which triggered
the event.

Note that on most platforms, `'rename'` is emitted whenever a filename appears
or disappears in the directory.

Also note the listener callback is attached to the `'change'` event fired by
[`fs.FSWatcher`][], but it is not the same thing as the `'change'` value of
`eventType`.

