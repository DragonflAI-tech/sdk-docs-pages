---
layout: default
title: DragonflAI SDK installation
parent: iOS documentation v1.5.0
---
# DragonflAI SDK for iOS

## XCFramework version

The SDK is now supplied as an `xcframework`, including support for the native M1 Simulator.

A 'fat', or universal, `.framework` is also still available, if this better suits your build process.

## Install the SDK using Cocoapods

We currently support integration via [CocoaPods](https://cocoapods.org). Links for manual integration are in the next section.

The DragonflAI SDK is hosted in our private CocoaPods repository.    

### Add the DragonflAI pod as a dependency

1. add the source `source 'https://api.dragonflai.co/repo/Nudity-SDK/cocoapods/CocoaPods-Podspecs.git'`. 

    You may also need to explicitly add the CocoaPods default CDN source when adding a private source,
    i.e. `source 'https://cdn.cocoapods.org/'`  
    Alternatively, if your pod setup still uses the git-based trunk source, you can continue to use that, but 
    the [CDN version is faster](https://blog.cocoapods.org/CocoaPods-1.8.0-beta/). 

2. Add an entry to your `~/.netrc` file

    Create or edit `.netrc` in your home directory, and add an entry for the DragonflAI server:

    ```
    machine api.dragonflai.co
    login [put your API key here]
    password 0000
    ```

    Make sure to edit this to include your own API key!

3. add the dependency `pod 'DragonflAI'`. 

    ```rb
    pod 'DragonflAI', '1.4.3'
    ```

    Or, for the legacy fat/universal framework, use `pod 'DragonflAI.universal'`. 

    See the [CocoaPods docs](https://guides.cocoapods.org/syntax/podfile.html#pod) for ways to control the version used.

4. add the post-install step to ensure our dependencies are built correctly to link with the DragonflAI SDK. 

    If you already have a post-install block you will need to combine it with ours, as there can be only one.
    
    ```ruby
    # DragonflAI post-install step
    post_install do |installer|
      puts "Performing post-install step for DragonflAI integration"
      installer.pods_project.targets.each do |target|
        if ['TensorFlowLiteSwift', 'PromiseKit'].include? target.name
          puts "Setting BUILD_LIBRARY_FOR_DISTRIBUTION = YES for " + target.name
          target.build_configurations.each do |config|
            config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
          end
        end
      end
    end  
    ```
    
    *See steps 1-4 together in the Podfile example below.*

5. To update your workspace, run `bundle exec pod install` or `pod install` in the terminal as usual.
    
6. If prompted in the terminal, enter your **API Key**, which you can find at our customer portal, 
   as the **username** to access `api.dragonflai.co`. 
   If a **password** is requested, use `0000`. See example output below.
   
   CocoaPods (via git) will save these credentials in the MacOS Keychain, so you should not be prompted again.     


##### Example Podfile:

```ruby 
platform :ios, '12.0'

source 'https://cdn.cocoapods.org/'
source 'https://api.dragonflai.co/repo/Nudity-SDK/cocoapods/CocoaPods-Podspecs.git'

target 'YourApp' do
  # ...

  # Pods for DragonflAI 
  pod 'DragonflAI'

  # ...
  
  # DragonflAI post-install step
  post_install do |installer|
    puts "Performing post-install step for DragonflAI integration"
    installer.pods_project.targets.each do |target|
      if ['TensorFlowLiteSwift', 'PromiseKit'].include? target.name
        puts "Setting BUILD_LIBRARY_FOR_DISTRIBUTION = YES for " + target.name
        target.build_configurations.each do |config|
          config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
        end
      end
    end
  end  
  
  # ...
end
```

##### Example terminal output:

When accessing our repo for the first time on a dev machine, the credentials may be requested as below.

`ffffffffffffffffffffffffffffffff` is not a real API Key / username!

```bash
$ bundle exec pod install --repo-update
Updating local specs repositories

CocoaPods 1.10.1 is available.
To update use: `gem install cocoapods`

For more information, see https://blog.cocoapods.org and the CHANGELOG for this version at https://github.com/CocoaPods/CocoaPods/releases/tag/1.10.1

  $ /usr/bin/git -C /Users/mobiledev/.cocoapods/repos/dragonflai-repo-nudity-sdk-cocoapods-ios-cocoapods-podspecs fetch origin
  --progress
Username for 'https://api.dragonflai.co': ffffffffffffffffffffffffffffffff
Password for 'https://d2359490563c00bedf67fc4e9ba3eb8e@api.dragonflai.co': 
  $ /usr/bin/git -C /Users/mobiledev/.cocoapods/repos/dragonflai-repo-nudity-sdk-cocoapods-ios-cocoapods-podspecs rev-parse --abbrev-ref
  HEAD
  master
  $ /usr/bin/git -C /Users/mobiledev/.cocoapods/repos/dragonflai-repo-nudity-sdk-cocoapods-ios-cocoapods-podspecs reset --hard
  origin/master
  HEAD is now at b02e238 Adding version '1.3.0'
Analyzing dependencies
[...]
```

## Install the SDK manually

We recommend using Cocoapods as the SDK's dependencies are not straightforward to integrate manually.

You can download the SDK directly:
 - [xcframework](https://api.dragonflai.co/repo/Nudity-SDK/apple/DragonflAI/1.4.3/DragonflAI.xcframework.zip)
 - or [legacy fat/universal framework](https://api.dragonflai.co/repo/Nudity-SDK/apple/DragonflAI/1.4.3/DragonflAI.universal.zip)

To integrate drag the contents of the zip archive into xcode. 

N.B. you will also need to provide the dependencies:

 - [PromiseKit](https://github.com/mxcl/PromiseKit) ~= 6.13 
 - [TensorFlowLiteC](https://www.tensorflow.org) == 2.5.0 
   - [as xcframework required for xcframework version of SDK](https://api.dragonflai.co/repo/Nudity-SDK/apple/TensorFlowLiteC/2.5.0/TensorFlowLiteC.xcframework.zip)

## Add algorithm assets to your project

The algorithm assets are large files which are distributed separately from the SDK. 

For the current SDK version 1.4.x this asset is `nudity7`

```
nudity7.dfai
```

The project location is not critical, but you may want to put this in a `DragonflAI` folder with your other bundled data or assets.


