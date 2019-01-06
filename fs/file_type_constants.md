
以下常量适用于 [`fs.Stats`] 对象的 `mode` 属性，用于决定文件的类型。

<table>
  <tr>
    <th>常量</th>
    <th>说明</th>
  </tr>
  <tr>
    <td><code>S_IFMT</code></td>
    <td>用于提取文件类型代码的位掩码。</td>
  </tr>
  <tr>
    <td><code>S_IFREG</code></td>
    <td>表示常规文件。</td>
  </tr>
  <tr>
    <td><code>S_IFDIR</code></td>
    <td>表示目录。</td>
  </tr>
  <tr>
    <td><code>S_IFCHR</code></td>
    <td>表示面向字符的设备文件。</td>
  </tr>
  <tr>
    <td><code>S_IFBLK</code></td>
    <td>表示面向块的设备文件。</td>
  </tr>
  <tr>
    <td><code>S_IFIFO</code></td>
    <td>表示 FIFO 或管道。</td>
  </tr>
  <tr>
    <td><code>S_IFLNK</code></td>
    <td>表示符号链接。</td>
  </tr>
  <tr>
    <td><code>S_IFSOCK</code></td>
    <td>表示套接字。</td>
  </tr>
</table>

