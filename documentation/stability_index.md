
<!--type=misc-->

文档中有每个章节的稳定性标志。
Node.js 的 API 仍会有少量变化，但随着发展，部分 API 会更稳定可靠。
有些 API 久经验证、且被大量依赖，它们几乎不会再变化。
也有些 API 是新增的、或试验的、或被认定为有风险且正在被重新设计中的。

稳定性指数如下：

```txt
稳定性: 0 - 废弃的
这个特性被认定为存在问题，且可能会计划修改。
不要依赖该特性。
使用该特性可能会产生警告信息。
不要指望该特性会有主版本间的向后兼容。
```

```txt
稳定性: 1 - 试验的
This feature is still under active development and subject to non-backwards
compatible changes, or even removal, in any future version. Use of the feature
is not recommended in production environments. Experimental features are not
subject to the Node.js Semantic Versioning model.
```

*Note*: Caution must be used when making use of `Experimental` features,
particularly within modules that may be used as dependencies (or dependencies
of dependencies) within a Node.js application. End users may not be aware that
experimental features are being used, and therefore may experience unexpected
failures or behavioral changes when changes occur. To help avoid such surprises,
`Experimental` features may require a command-line flag to explicitly enable
them, or may cause a process warning to be emitted. By default, such warnings
are printed to `stderr` and may be handled by attaching a listener to the
`process.on('warning')` event.

```txt
稳定性: 2 - 稳定的
这个特性已被证明是符合要求的。
与 npm 生态系统的兼容性是一个高优先级，除非绝对必要否则不会变化。
```

