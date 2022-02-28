---
layout: default
title: Account
has_children: true
parent: API (Android)
---

# Account

`class Account`

Represents your customer account as an SDK user

### Constructors

| [&lt;init&gt;](-init-.html) | Create an account programmatically.`Account(key: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)`, secret: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)`)`<br>Create an account using the values found in the bundle, e.g. set in `AndroidManifest.xml``Account(metaData: `[`Bundle`](https://developer.android.com/reference/android/os/Bundle.html)`)` |

### Properties

| [key](key.html) | Your customer account key`val key: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html) |
| [secret](secret.html) | Your customer account secret`val secret: `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html) |

### Functions

| [toString](to-string.html) | Log an Account instance with truncated key and secret.`fun toString(): `[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html) |

