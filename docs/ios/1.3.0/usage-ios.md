---
layout: default
title: DragonflAI SDK usage
parent: iOS documentation v1.3
---
# DragonflAI SDK for iOS

## Usage

### Initialising

DragonflAI is a commercial product and requires licensing details during framework initialization. This should have been provided alongside this documentation, but if not please contact <mailto:support@dragonflai.co>.

Initialise early in your app's startup. 
For example here in the `AppDelegate` method `application:willFinishLaunchingWithOptions:`, we call `useAccount()` with our license details. 


```swift
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, willFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        
        // To see debug log messages, pass a debug logger.
        // NB: limit use to debug builds 
        DragonflAICore.useLogger(logger: ConsoleLogger(logLevel: .debug))
        
        let account = Account(key: "your_key", secret: "your_secret")        
        DragonflAICore.useAccount(account)
        
        return true
    }
}
```

This is a basic example. You may wish to keep your credentials in config rather than code.

### Moderating an image

Create a `Moderator` instance, and pass an image to `moderate()`.


##### Example using a closure:

⚠️ You should assume the closure is **not** called on the main queue, and dispatch UI updates accordingly.

```swift
let image: UIImage = [your choice of image]

Moderator().moderate(image) { (moderationResult) in
            
    // update model
    
    DispatchQueue.main.async {
        // update UI 
    }
}
```


### Customising a Moderator 

`Moderator` can take an optional config object if you don't want to use the defaults.
They can be retained and reused.

Parameters for current version 1.2.x :
* `blockThreshold` (see API reference)

```swift
let config = Moderator.Config(blockThreshold: 50)
let moderator = Moderator(config: config)
```

