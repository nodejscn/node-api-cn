
以下常量适用于 [`fs.access()`]。

<table>
  <tr>
    <th>常量</th>
    <th>说明</th>
  </tr>
  <tr>
    <td><code>F_OK</code></td>
    <td>表明文件对调用进程可见。
    这对于判断文件是否存在很有用，但对 <code>rwx</code> 权限没有任何说明。 
    如果未指定模式，则默认值为该值。
    </td>
  </tr>
  <tr>
    <td><code>R_OK</code></td>
    <td>表明调用进程可以读取文件。</td>
  </tr>
  <tr>
    <td><code>W_OK</code></td>
    <td>表明调用进程可以写入文件。</td>
  </tr>
  <tr>
    <td><code>X_OK</code></td>
    <td>表明调用进程可以执行文件。
    在 Windows 上无效（表现得像 <code>fs.constants.F_OK</code>）。
    </td>
  </tr>
</table>

