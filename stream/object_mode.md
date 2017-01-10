
All streams created by Node.js APIs operate exclusively on strings and `Buffer`
objects. It is possible, however, for stream implementations to work with other
types of JavaScript values (with the exception of `null`, which serves a special
purpose within streams). Such streams are considered to operate in "object
mode".

Stream instances are switched into object mode using the `objectMode` option
when the stream is created. Attempting to switch an existing stream into
object mode is not safe.

