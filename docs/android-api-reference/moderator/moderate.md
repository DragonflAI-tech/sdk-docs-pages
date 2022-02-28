---
layout: default
title: moderate
has_children: false
parent: Moderator
grand_parent: API (Android)
---

# moderate

`suspend fun moderate(bitmap: `[`Bitmap`](https://developer.android.com/reference/android/graphics/Bitmap.html)`): Result<`[`Analysis`](../-analysis/index.html)`, `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html)`>`

Suspend function to moderate a bitmap image

### Parameters

`bitmap` - the input image

**Return**
`Result` of analysis

`fun moderate(bitmap: `[`Bitmap`](https://developer.android.com/reference/android/graphics/Bitmap.html)`, callback: Callback): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)

Start moderating a bitmap image

This callback-based method is provided for integration from `Java`, and avoids the use
of Result and Coroutines.

### Parameters

`bitmap` - the input image

`callback` - with an `Analysis` or `Error`