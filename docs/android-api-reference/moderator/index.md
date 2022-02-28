---
layout: default
title: Moderator
has_children: true
parent: API (Android)
---


# Moderator

`class Moderator`

Pass images to a Moderator to get a verdict on the contents

A moderator can be retained and used to moderate images
for as long as moderation is required with the same config.

### Types

| [Callback](-callback/index.html) | Provide a `Callback` to the callback-based `moderate()` method.`interface Callback` |
| [Config](-config/index.html) | A provider of configuration settings`interface Config` |

### Exceptions

| [ConvertingInputImageError](-converting-input-image-error/index.html) | Moderation error: Input image could not be converted by preprocessor`class ConvertingInputImageError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |
| [LoadingBundledModelError](-loading-bundled-model-error/index.html) | Moderation error: Model could not be loaded from bundle`class LoadingBundledModelError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |
| [RunningModelError](-running-model-error/index.html) | Moderation error: Model produced no output`class RunningModelError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |

### Constructors

| [&lt;init&gt;](-init-.html) | Creates a Moderator with default Config.`Moderator(context: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`)`<br>Pass images to a Moderator to get a verdict on the contents`Moderator(context: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`, config: Config)` |

### Functions

| [moderate](moderate.html) | Suspend function to moderate a bitmap image`suspend fun moderate(bitmap: `[`Bitmap`](https://developer.android.com/reference/android/graphics/Bitmap.html)`): Result<`[`Analysis`](../-analysis/index.html)`, `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html)`>`<br>Start moderating a bitmap image`fun moderate(bitmap: `[`Bitmap`](https://developer.android.com/reference/android/graphics/Bitmap.html)`, callback: Callback): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html) |

