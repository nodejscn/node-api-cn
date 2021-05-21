
On Windows, Node.js follows the concept of per-drive working directory. This
behavior can be observed when using a drive path without a backslash. For
example `fs.readdirSync('C:\\')` can potentially return a different result than
`fs.readdirSync('C:')`. For more information, see
[this MSDN page][MSDN-Rel-Path].

