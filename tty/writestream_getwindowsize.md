<!-- YAML
added: v0.7.7
-->
* Returns: {number[]}

`writeStream.getWindowSize()` returns the size of the [TTY](tty.html)
corresponding to this `WriteStream`. The array is of the type
`[numColumns, numRows]` where `numColumns` and `numRows` represent the number
of columns and rows in the corresponding [TTY](tty.html).

