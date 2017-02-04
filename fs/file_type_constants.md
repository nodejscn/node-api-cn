
以下常量用于 [`fs.Stats`] 对象中用于决定一个文件的类型的 `mode` 属性。

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>S_IFMT</code></td>
    <td>用于提取文件类型码的位掩码。</td>
  </tr>
  <tr>
    <td><code>S_IFREG</code></td>
    <td>表示一个常规文件的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFDIR</code></td>
    <td>表示一个目录的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFCHR</code></td>
    <td>表示一个面向字符的设备文件的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFBLK</code></td>
    <td>表示一个面向块的设备文件的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFIFO</code></td>
    <td>表示一个 FIFO/pipe 的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFLNK</code></td>
    <td>表示一个符号链接的文件类型常量。</td>
  </tr>
  <tr>
    <td><code>S_IFSOCK</code></td>
    <td>表示一个 socket 的文件类型常量。</td>
  </tr>
</table>

