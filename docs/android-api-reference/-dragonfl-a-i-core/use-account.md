---
layout: default
title: user-account
has_children: false
parent: Dragonflai-Core
grand_parent: API (Android)
---

# useAccount

`fun useAccount(fromContext: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)

Initialize before using SDK methods, ideally during app startup, for best performance.

Uses account details from Manifest.

### Parameters

`fromContext` - e.g. passing `this` in your Application class’s onCreate()`fun useAccount(account: `[`Account`](../-account/index.html)`? = null, context: `[`Context`](https://developer.android.com/reference/android/content/Context.html)`): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)

Initialize before using SDK methods, ideally during app startup, for best performance.

Uses injected account details instead of loading from Manifest.

### Parameters

`account` - an Account instance

`context` - e.g. passing `this` in your Application class’s onCreate()