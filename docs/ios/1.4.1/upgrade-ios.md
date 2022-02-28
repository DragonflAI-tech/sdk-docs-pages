---
layout: default
title: DragonflAI SDK upgrading
parent: iOS documentation v1.4.1
---
# DragonflAI SDK for iOS

## Upgrading from version 1.3.x

### Update the pod version in your Podfile

E.g. for any iteration of `1.4`

```rb
  pod 'DragonflAI', '~> 1.4'
```

And run a (`bundle exec`) `pod install`

#### Troubleshooting

You may get an error such as this:

```bash
Analyzing dependencies
[!] CocoaPods could not find compatible versions for pod "DragonflAI":
  In Podfile:
    DragonflAI (~> 1.4)

None of your spec sources contain a spec satisfying the dependency: `DragonflAI (~> 1.4)`.

You have either:
 * out-of-date source repos which you can update with `pod repo update` or with `pod install --repo-update`.
 * mistyped the name or version.
 * not added the source repo that hosts the Podspec to your Podfile.
```

If so, follow the suggestion given to "update with `pod repo update` or with `pod install --repo-update`."

### Use a newer algorithm

#### 1. Replace the asset 

* Remove `nudity1.dfai` from your project
* Add `nudity7.dfai` to your project (note the changed number)

#### 2. Change code that creates `Moderator`

* Change `Moderator()` to `Moderator(algorithm: .nudity7)` to use the new algorithm asset
* `Moderator()` continues to compile and work — however it will use the older `nudity1` algorithm asset only

