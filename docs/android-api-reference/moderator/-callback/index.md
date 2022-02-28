---
layout: default
title: Callback
has_children: true
parent: Moderator
grand_parent: API (Android)
---


# Callback

`interface Callback`

Provide a `Callback` to the callback-based `moderate()` method.

This is provided primarily for simpler `Java` integration.

### Functions

| [onAnalysis](on-analysis.html) | A moderation `Analysis` was produced successfully`abstract fun onAnalysis(analysis: `[`Analysis`](../../-analysis/index.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html) |
| [onError](on-error.html) | The moderation result is an `Error``abstract fun onError(error: `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html) |

