<!-- YAML
added: v0.7.7
-->

* `stream` {Writable}
* `dir` {number}
  * `-1` - to the left from cursor
  * `1` - to the right from cursor
  * `0` - the entire line

The `readline.clearLine()` method clears current line of given [TTY][] stream
in a specified direction identified by `dir`.


