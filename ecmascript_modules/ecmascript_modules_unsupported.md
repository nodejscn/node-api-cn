<table>
  <tr>
    <th>特性</th>
    <th>原因</th>
  </tr>
  <tr>
    <td><code>require('./foo.mjs')</code></td>
    <td>ES模块具有不同的加载方式，使用 `import()`语言标准</td>
  </tr>
  <tr>
    <td><code>import()</code></td>
    <td>等待在Node.js中使用更加新的V8版本</td>
  </tr>
  <tr>
    <td><code>import.meta</code></td>
    <td>等待V8实现</td>
  </tr>
  <tr>
    <td>Loader Hooks</td>
    <td>等待Node.js EP创建/达成共识</td>
  </tr>
</table>