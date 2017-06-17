
<!--type=misc-->

所有这些方法都将 [`Buffer`][], [`TypeArray`][], [`DataView`][], 或者字符串作为第一个
参数, 一个回调函数作为可选的第二个参数提供给 `zlib` 类, 会在 `callback(error, result)`
中调用.

每一个方法相对应的都有一个接受相同参数, 但是没有回调的 `*Sync` 版本. 

