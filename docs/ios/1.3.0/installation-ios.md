---
layout: default
title: DragonflAI SDK installation
parent: iOS documentation v1.3
---
# DragonflAI SDK for iOS

## Universal Framework version

The SDK is currently supplied as a 'fat', or universal, framework. 

We hope to add XCFramework support soon.

## Install the SDK using Cocoapods

We currently support integration via [CocoaPods](https://cocoapods.org)

Contact us for support if you need manual integration or other dependency managers.

The DragonflAI SDK is hosted in our private CocoaPods repository.    

### Add the DragonflAI pod as a dependency

1. add the source `source 'https://api.dragonflai.co/repo/Nudity-SDK/cocoapods/iOS-CocoaPods-Podspecs.git'`. 

    You may also need to explicitly add the CocoaPods default CDN source when adding a private source,
    i.e. `source 'https://cdn.cocoapods.org/'`  
    Alternatively, if your pod setup still uses the git-based trunk source, you can continue to use that, but 
    the [CDN version is faster](https://blog.cocoapods.org/CocoaPods-1.8.0-beta/). 

2. add the dependency `pod 'DragonflAI'`. 
See the [CocoaPods docs](https://guides.cocoapods.org/syntax/podfile.html#pod) for ways to control the version used.

3. add the post-install step to ensure our dependencies are built correctly to link with the DragonflAI SDK. 

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
    
    *See steps 1-3 together in the Podfile example below.*

4. To update your workspace, run `bundle exec pod install` or `pod install` in the terminal as usual.
   
   We strongly recommend [using](https://number42.de/blog/2018/05/22/rbenv-2018-05-22-rbenv.html) 
   `rbenv` and `bundler` to control the environment CocoaPods runs in and avoid surprises in the long term.
    
5. When prompted in the terminal, enter your **API Key**, which you can find at our customer portal, 
   as the **username** to access `api.dragonflai.co`. 
   If a **password** is requested, use `0000`. See example output below.
   
   CocoaPods (via git) will save these credentials in the MacOS Keychain, so you should not be prompted again.     


##### Example Podfile:

```ruby 
platform :ios, '12.0'

source 'https://cdn.cocoapods.org/'
source 'https://api.dragonflai.co/repo/Nudity-SDK/cocoapods/iOS-CocoaPods-Podspecs.git'

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

When accessing our repo for the first time on a dev machine, the credentials are requested as below.

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

## Add algorithm assets to your project

The algorithm assets are large files which are distributed separately from the SDK. 
You can find them in the [Downloads area of our customer portal](https://portal.dragonflai.co/downloads).   

For the current SDK version 1.3.x this asset is `nudity1`

```
nudity1.dfai
```

The project location is not critical, but you may want to put this in a `DragonflAI` folder with your other bundled data or assets.


