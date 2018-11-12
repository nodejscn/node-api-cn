
以下常量用于 [`fs.access()`]。

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>F_OK</code></td>
    <td>表明文件对于调用进程是可见的。
    主要用于检测文件是否存在，但不会表明 <code>rwx</code> 权限。
    如果没有指定模式则默认为该模式。
    </td>
  </tr>
  <tr>
    <td><code>R_OK</code></td>
    <td>表明文件可被调用进程读取。</td>
  </tr>
  <tr>
    <td><code>W_OK</code></td>
    <td>表明文件可被调用进程写入。</td>
  </tr>
  <tr>
    <td><code>X_OK</code></td>
    <td>表明文件可被调用进程执行。
    Windows 上无效（效果同 <code>fs.constants.F_OK</code>）。
    </td>
  </tr>
</table>

