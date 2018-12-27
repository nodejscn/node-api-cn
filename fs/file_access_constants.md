
以下常量用于 [`fs.access()`]。

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>F_OK</code></td>
    <td>文件可见。
    用于检查文件是否存在，但不会表明 <code>rwx</code> 权限。
    </td>
  </tr>
  <tr>
    <td><code>R_OK</code></td>
    <td>文件可读。</td>
  </tr>
  <tr>
    <td><code>W_OK</code></td>
    <td>文件可写。</td>
  </tr>
  <tr>
    <td><code>X_OK</code></td>
    <td>文件可执行。
    在 Windows 上无效（效果同 <code>fs.constants.F_OK</code>）。
    </td>
  </tr>
</table>

