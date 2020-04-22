
<!--type=misc-->

`fs.watch` 的 API 在各个平台上并非 100％ 一致，在某些情况下不可用。

仅在 macOS 和 Windows 上支持 `recursive` 选项。
当在不支持该选项的平台上使用该选项时，则会抛出 `ERR_FEATURE_UNAVAILABLE_ON_PLATFORM` 异常。

在 Windows 上，如果监视的目录被移动或重命名，则不会触发任何事件。 
当监视的目录被删除时，则报告 `EPERM` 错误。

