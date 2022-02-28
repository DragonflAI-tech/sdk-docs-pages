---
layout: default
title: DragonflAI SDK usage
parent: iOS documentation v1.4.1
---
# DragonflAI SDK for iOS

## Usage

### Initialising

DragonflAI is a commercial product and requires licensing details during framework initialization. This should have been provided alongside this documentation, but if not please contact <mailto:support@dragonflai.co>.

Initialise early in your app's startup. 
For example here in the `AppDelegate` method `application:willFinishLaunchingWithOptions:`, we call [`useAccount()`](api-reference/Classes/DragonflAICore.html) with our license details. 


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

Create a [`Moderator`](api-reference/Classes/Moderator.html) instance, and pass an image to `moderate()`.

##### Basic example using a closure to handle the result:


```swift
let image: UIImage = [your choice of image]

Moderator(algorithm: .nudity1).moderate(image) { (moderationResult) in
            
    // *** update model in background thread ***

    // *** example of expanding result ***
    switch moderationResult {
    case .success(let success):
        switch success.analysis.decision {
        case .ok:
            // moderator allowed this image
        case .blocked:
            // moderator blocked this image
        @unknown default:
            // this covers any future return types 
        }
    case .failure(let error):
        // moderation error
    }
    
    DispatchQueue.main.async {
        // *** update UI in main thread ***
    }
}
```

⚠️ You should assume the closure is **not** called on the main queue, and dispatch UI updates accordingly.

##### Configuring a moderator

You may want to configure and reuse a [`Moderator`](api-reference/Classes/Moderator.html) instance instead of creating it every time.

It can take an optional [AlgorithmConfig](/api-reference/Structs/AlgorithmConfig.html) object if you don't want to use the defaults.

```swift
let config = AlgorithmConfig(blockThreshold: 50)
let moderator = Moderator(algorithm: .nudity1, config: config)

// ...

moderator.moderate(image) { (moderationResult) in 
    // use result
}
```

##### Promises (PromiseKit)

You can also get the results via PromiseKit promises.

```swift
moderator?.moderate(image)
    .map { (success: ModeratorSuccess) in
        // use analysis and metadata
    }
    .catch { error in
        // handle error
    }
```

### Moderating a video stream

Streams of images can also be moderated in v1.4+. Typically these come from the device cameras and are passed to a codec for streaming or real-time communication.

##### Creating a StreamModerator

Get a [`StreamModerator`](api-reference/Classes/StreamModerator.html) by asking a [`Moderator`](api-reference/Classes/Moderator.html) to `createStreamModerator()`

```swift
class MyClass {
    private var streamModerator: StreamModerator?

    init() {
        let moderator = Moderator(algorithm: .nudity1)
        streamModerator = moderator.createStreamModerator()
        streamModerator?.delegate = self    
    }
}
```

##### Supplying stream frames

Pass the frames, e.g. from the camera, to the `process(frame:)` method.

```swift
extension MyClass: AVCaptureVideoDataOutputSampleBufferDelegate {    
  func captureOutput(_ output: AVCaptureOutput, didOutput sampleBuffer: CMSampleBuffer, from connection: AVCaptureConnection) {

    let pixelBuffer: CVPixelBuffer? = CMSampleBufferGetImageBuffer(sampleBuffer)

    guard let pixelBuffer = pixelBuffer else {
      return
    }

    streamModerator?.process(frame: pixelBuffer)

    // pass pixelBuffer to codec (dependent on moderation result) 
  }

}
```

##### Getting results

To get results, assign a delegate, typically the same class.

```swift
extension MyClass: StreamModeratorDelegate {
    func moderatorDidProduceNewResult(_ moderator: StreamModerator,
                                      result moderationResult: ModeratorResult) {
        
        guard moderator == self.streamModerator else {
            return
        }

        // use moderationResult
    }

    func moderatorDidDropFrame(_ moderator: StreamModerator) {
        // dropped frame
    }
}
```

##### Getting stream statistics

The [`StreamModerator`](api-reference/Classes/StreamModerator.html) can provide statistics on the number of frames it is receiving and processing.

```swift
func printStats() {
    print("Input FPS: \(streamModerator.inputFramesPerSecond) / Processed FPS: \(moderator.processedFramesPerSecond)")
}
```

For consistent results, reset those stats when starting or resuming a session, so periods with no frames are not included.

```swift
func startVideoSession() {
    // ...

    streamModerator?.resetFPSStats()

    // ...
}
```

