---
layout: default
title: DragonflAI SDK upgrading
parent: iOS documentation v1.4.3
---
# DragonflAI SDK for iOS

## Upgrading from version 1.4.x

These instructions assume you want to switch to using `xcframework` builds.

### Change the DragonflAI pod repo URL in your Podfile

The new repo is: 

```rb
source 'https://api.dragonflai.co/repo/Nudity-SDK/cocoapods/CocoaPods-Podspecs.git'
```

This replaces the old `iOS-CocoaPods-Podspecs.git` URL.

### Add an entry to your `~/.netrc` file

Create or edit `.netrc` in your home directory, and add an entry for the DragonflAI server:

```
machine api.dragonflai.co
login [put your API key here]
password 0000
```

Make sure to edit this to include your own API key.

#### Troubleshooting

Netrc will not use the `~/.netrc` file if its permissions are too broad. Ensure it is only readable by yourself.



