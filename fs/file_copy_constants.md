
The following constants are meant for use with [`fs.copyFile()`][].

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>COPYFILE_EXCL</code></td>
    <td>If present, the copy operation will fail with an error if the
    destination path already exists.</td>
  </tr>
  <tr>
    <td><code>COPYFILE_FICLONE</code></td>
    <td>If present, the copy operation will attempt to create a
    copy-on-write reflink. If the underlying platform does not support
    copy-on-write, then a fallback copy mechanism is used.</td>
  </tr>
  <tr>
    <td><code>COPYFILE_FICLONE_FORCE</code></td>
    <td>If present, the copy operation will attempt to create a
    copy-on-write reflink. If the underlying platform does not support
    copy-on-write, then the operation will fail with an error.</td>
  </tr>
</table>

