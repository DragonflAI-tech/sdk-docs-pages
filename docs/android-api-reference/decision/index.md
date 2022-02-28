---
layout: default
title: Decision
has_children: true
parent: API (Android)
---

# DecisionOK

`object DecisionOK : `[`Decision`](index.html)

The input has passed moderation

# DecisionBlocked

`class DecisionBlocked : `[`Decision`](../index.html)

The input has failed moderation

### Constructors

| [&lt;init&gt;](-init-.html) | The input has failed moderation`DecisionBlocked(title: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)`, probabilityPercent: `[`Int`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-int/index.html)`)` |

### Properties

| [probabilityPercent](probability-percent.html) | the confidence that this content is in the image`val probabilityPercent: `[`Int`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-int/index.html) |
| [title](title.html) | of the main content the input has failed on`val title: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html) |

### Functions

| [toString](to-string.html) | `fun toString(): `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html) |

