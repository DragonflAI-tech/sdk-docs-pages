---
layout: default
title: DragonflAI SDK usage
parent: v1.3.3
grand_parent: Android
---
# DragonflAI SDK for Android

## Usage

### Initialising

DragonflAI is a commercial product and requires licensing details during framework initialization. This should have been provided alongside this documentation, but if not please contact <mailto:support@dragonflai.co>.

There are two options for providing your license details to the SDK, **programmatically** or **by configuration**.

#### Initialise by configuration
Place your license details in your app’s `AndroidManifest.xml` (these values are just examples):

```xml
<application>
	<meta-data
        android:name="co_dragonflai_license_key"
        android:value="ffffffffffffffffffffffffffffffff" />
    <meta-data
        android:name="co_dragonflai_license_secret"
        android:value="ffffffff-ffff-ffff-ffff-ffffffffffff" />
</application>
```

Initialise early in your app's startup. For example here in the `Application` class's `onCreate()`, we call `useAccount` with our context to use the details from the manifest. It is also possible to set the account details programatically.

```kotlin
class App : Application() {
    override fun onCreate() {
        super.onCreate()

        // Initialise DragonflAI API to allow it to check licensing details
        // This will take place asynchronously in the background
        DragonflAICore.useAccount(this)
    }
}
```

#### Initialise programmatically

Initialise early in your app's startup.
For example here in the `Application` class's `onCreate()`, we call `useAccount` with our license details and context.


```kotlin
class App : Application() {
    override fun onCreate() {
        super.onCreate()

        // Initialise DragonflAI API to allow it to check licensing details
        // This will take place asynchronously in the background
        val account = Account(
            "ffffffffffffffffffffffffffffffff",
            "ffffffff-ffff-ffff-ffff-ffffffffffff")
        DragonflAICore.useAccount(account, this)
    }
}
```


### Moderating an image

First create a `Moderator` instance.

```kotlin
val moderator = Moderator(this)
```

This can take an optional config object if you don't want to use the defaults.

```kotlin
val moderator = Moderator(this, config = object :Moderator.Config {
    override val blockThreshold = 70
})
```

Pass images to the `Moderator`, and the analysis will be returned asynchronously.

Example using Kotlin's coroutines:

```kotlin
MainScope().launch(Dispatchers.IO) {

    // Load image in the background
    val bitmap = BitmapFactory.decodeFile(imagePath)
    if (bitmap != null) {

        // Moderate your image
        val result = moderator.moderate

        // Use the result
        view_model = when(analysis.decision) {
            Decision.DecisionOK -> {
                "Non-nude"
            }
            is Decision.DecisionNudity -> {
                val d = analysis.decision as Decision.DecisionNudity
                "Nude: ${d.title} @\u00A0${d.probabilityPercent}%"
            }
        }

        MainScope().launch {
            // Update the UI
        }
    }
}
```

Example using a callback from Java:

```java
moderator.moderate(bitmap,  new Moderator.Callback() {
    @Override
    public void onAnalysis(@NotNull Analysis analysis) {
        Decision decision = analysis.getDecision();
        if (decision instanceof Decision.DecisionNudity) {
            Decision.DecisionNudity nudity = (Decision.DecisionNudity) decision;
            int pc = nudity.getProbabilityPercent();
            String title = nudity.getTitle();
            // Handle Nudity
            // E.g. display message and block user action
        } else if (decision instanceof  Decision.DecisionOK) {
            // Handle OK
            // E.g. allow user action to proceed
        }
    }

    @Override
    public void onError(@NotNull Error error) {
        // handle error
        // E.g. display message
    }
});
```


