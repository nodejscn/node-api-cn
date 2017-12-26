<!--
added: v8.0.0
-->

[`Serializer`][]的子类，用来将`TypedArray`(尤其是[`Buffer`][])和`Dataview`序列化成一个宿主对象，并且只会存储部分他们在底层实际指向的`ArrayBuffer`。
