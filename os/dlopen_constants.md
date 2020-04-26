
如果在操作系统上可用，则以下常量在 `os.constants.dlopen` 中导出。 
有关详细信息，请参见 dlopen(3) 信息。

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>RTLD_LAZY</code></td>
    <td>执行延迟绑定。 Node.js 默认设置此标志。</td>
  </tr>
  <tr>
    <td><code>RTLD_NOW</code></td>
    <td>在 dlopen(3) 返回之前解析库中的所有未定义符号。</td>
  </tr>
  <tr>
    <td><code>RTLD_GLOBAL</code></td>
    <td>库定义的符号将可用于后续加载的库的符号解析。</td>
  </tr>
  <tr>
    <td><code>RTLD_LOCAL</code></td>
    <td>与 <code>RTLD_GLOBAL</code> 相反。 如果未指定任何标志，则这是默认行为。</td>
  </tr>
  <tr>
    <td><code>RTLD_DEEPBIND</code></td>
    <td>使一个独立的库使用自己的符号，而不是先前加载的库中的符号。</td>
  </tr>
</table>

