---
layout: default
title: DragonflAI SDK usage
parent: v1.5.0
grand_parent: Android
---
# DragonflAI SDK for Android

## Usage

### Initialising

DragonflAI is a commercial product and requires licensing details during framework initialization. This should have been provided alongside this documentation, but if not please contact <mailto:support@dragonflai.co>.

There are two options for providing your license details to the SDK, **programmatically** or **by configuration**. The former offers more customisation options.


#### Initialise programmatically

##### Account

Initialise early in your app's startup.
For example here in the `Application` class's `onCreate()`, we call `useAccount` with our license details and context.
Place your license details in the Account initialiser (these values are just examples).


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

##### License mode

###### Standard

The DragonflAI SDK can be used out of the box to moderate, and in the default `LicenseMode.STANDARD` mode it will use a unique ID per app install for licensing purposes. This is generated and maintained internally.

This strategy will opportunistically check the licensing server, if required, as early as possible. It aims to avoid running licensing checks during SDK use, i.e. avoiding delays to user initiated actions.

###### CustomerUserID

If you wish to link licensing user counts more closely to your users:
 - During initialisation, set the appropriate license mode i.e. `DragonflAICore.useLicenseMode(LicenseMode.CUSTOMER_USER_ID)`, *before* calling `useAccount()`. This will prevent licensing checks (and hence use of the SDK) until a user ID is provided.
 - When you have a unique ID for your user, e.g. following login, provide it to the SDK `DragonflAICore.useUserID($yourUniqueString$)`. This ID will be used for licensing until changed or reset to `nil`, persisting across restarts of your app.

##### Sending metrics

If you wish to participate in our metrics collection, to better understand the customer experience and help development of our algorithms, please get in touch so we can discuss the details, at <mailto:support@dragonflai.co>.

To send metrics, you need to opt in via the SDK: `DragonflAICore.sendMetrics(moderationTally: true)`. The default behaviour is not to send any metrics to the server.


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


