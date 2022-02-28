---
layout: default
title: with-license-check
has_children: true
parent: Dragonflai-Core
grand_parent: API (Android)
---

# withLicenseCheck

`suspend fun <T> withLicenseCheck(doThing: Deferred<Result<T, `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html)`>>): Result<T, `[`Error`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-error/index.html)`>`

Wraps a deferred future (e.g. moderation action) in a license check

### Parameters

`T` - our Result success type

`doThing` - an async/future Deferred Result&lt;T, Error&gt;

**Return**
Result&lt;T, Error&gt;

