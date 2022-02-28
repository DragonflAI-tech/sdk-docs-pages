---
layout: default
title: DragonflAI SDK installation
parent: v1.5.0
grand_parent: Android
---
# DragonflAI SDK for Android

## Install the SDK using Gradle

### Project build config

#### Kotlin

This SDK uses Kotlin so you must add the following to the **project-level** `build.gradle` if they are not already present:

```gradle
buildscript {
    ext.kotlin_version = "1.3.72"
    ...
    dependencies {
        ...
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```

#### Repository

This SDK is hosted in our Maven repository, which must also be added to the **project-level** `build.gradle`.

* Insert the repo **username** supplied to you, which is your **API Key**, you will find this in the portal.
* The **password** is always `0000`.

```gradle
allprojects {
    repositories {
        ...
        maven {
            url 'https://api.dragonflai.co/repo/Nudity-SDK/maven'
            credentials {
                username = "your_repo_username"
                password = "0000"
            }
        }
    }
}
```

⚠️ This is a basic example.
You may wish to store credentials in a global or project level `gradle.properties` file, rather than `build.gradle` where they will be stored in version control.

### App build config

#### Android config

DragonflAI SDK is supported on Android devices running API level 16 (Android 4.1) and newer, targeting the latest stable Android version 10 (API 29).
It also requires apps to enable Java 8 language features in order to build. Inside your **app-level** `build.gradle` file, make sure to have the following configuration:

```gradle
android {
    compileSdkVersion 29
    buildToolsVersion '29.0.3'

    defaultConfig {
        ...

        minSdkVersion 16
        targetSdkVersion 29
    }

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```

#### File compression

Compression must be disabled on certain files to enable DragonflAI to read them via memory mapping, in the **app-level** `build.gradle`.

```gradle
aaptOptions {
    // Compression must be disabled on certain files to enable DragonflAI
    noCompress "dragonflai"
}
```

#### The SDK

Add to your dependencies in the **app-level** `build.gradle`.

```gradle
dependencies {
    ...

    // DragonflAI SDK
    implementation "co.dragonflai.sdk:dragonflai-sdk:1.5.0"
}
```

#### Logging

The SDK uses SLF4J so you can configure any compatible framework to direct the log output in the **app-level** `build.gradle`.

For example, using [`logback`](http://logback.qos.ch) (this also requires a config file located at `assets/logback.xml`):

```gradle
dependencies {
    ...

    // logging
    // Any SLF4J compatible logging framework can be used to direct log output from the DragonflAI SDK
    // The configuration for this one can be found in `assets/logback.xml`
    implementation 'com.github.tony19:logback-android:2.0.0'
}
```



