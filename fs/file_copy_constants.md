
以下常量适用于 [`fs.copyFile()`]。

<table>
  <tr>
    <th>常量</th>
    <th>说明</th>
  </tr>
  <tr>
    <td><code>COPYFILE_EXCL</code></td>
    <td>如果目标路径已存在，则拷贝操作将失败。</td>
  </tr>
  <tr>
    <td><code>COPYFILE_FICLONE</code></td>
    <td>拷贝操作将尝试创建写时拷贝链接。
    如果底层平台不支持写时拷贝，则使用备选的拷贝机制。
    </td>
  </tr>
  <tr>
    <td><code>COPYFILE_FICLONE_FORCE</code></td>
    <td>拷贝操作将尝试创建写时拷贝链接。
    如果底层平台不支持写时拷贝，则拷贝操作将失败。
    </td>
  </tr>
</table>

