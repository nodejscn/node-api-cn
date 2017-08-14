Node.js有许多功能，使它更容易编写国际化程序.其中一些是：
- [ECMAScript语言规格][ECMA-262]中的本地化敏感或感知统一编码功能：
  - [`String.prototype.normalize()`][]
  - [`String.prototype.toLowerCase()`][]
  - [`String.prototype.toUpperCase()`][]
- [ECMAScript国际化API规格][ECMA-402] (aka ECMA-402)中的所有的功能：
  - [`Intl`][] 对象
  -本地化敏感的方法如[`String.prototype.localeCompare()`][] 和 [`Date.prototype.toLocaleString()`][]
- WHATWG URL解析器的[国际化域名 ] [ ]（IDN）的支持
- [ `要求（'buffer”）。transcode() ` ] [ ]
- 更准确的[REPL] [ ] 行编辑
- [`require('util').TextDecoder`][]

Node.js（及其背后的V8引擎）在原生的C / C++代码使用[ICU] [ ] 实施这些功能。
然而，其中一些为了支持世界的所有地区，需要一个非常大的ICU数据文件。
因为预计多数Node.js的用户将只使用ICU的功能的一小部分，Node.js默认设置了所有ICU的数据集的一个子集。
当建设或运行Node.js时提供了几个定制和扩展ICU数据集的选项。
