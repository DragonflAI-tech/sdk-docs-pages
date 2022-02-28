---
layout: default
title: Dragonflai-Core
has_children: true
parent: API (Android)
---

# DragonflAICore

`object DragonflAICore : LicenseProviding, Logging`

The DragonflAICore singleton manages central API functions.

Initialize it with app context before use, ideally during app startup, for best performance.

### Exceptions

| [BadAccountConfigError](-bad-account-config-error/index.html) | Error thrown by SDK methods, when configured with invalid or missing license details.`class BadAccountConfigError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |
| [CannotReachServerError](-cannot-reach-server-error/index.html) | Error thrown by SDK methods, when DragonflAI is unable to reach our licensing server.`class CannotReachServerError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |
| [NotLicensedError](-not-licensed-error/index.html) | Error thrown by SDK methods, when configured with invalid license details.`class NotLicensedError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |
| [UnexpectedExceptionError](-unexpected-exception-error/index.html) | Error thrown by SDK methods, when an underlying exception is not expected.`class UnexpectedExceptionError : `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html) |

### Properties

| [statusLiveData](status-live-data.html) | The current state of SDK licensing checks in observable form.`val statusLiveData: LiveData<`[`LicenseStatus`](../-license-status/index.html)`>` |

### Functions

| [useAccount](use-account.html) | Initialize before using SDK methods, ideally during app startup, for best performance.`fun useAccount(fromContext: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)<br>`fun useAccount(account: `[`Account`](../-account/index.html)`? = null, context: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html) |

