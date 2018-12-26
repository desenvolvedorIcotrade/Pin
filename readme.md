
# (PINRemoteImage)

## Fast, non-deadlocking parallel image downloader , and cache for iOS..

[![CocoaPods compatible](https://img.shields.io/cocoapods/v/PINRemoteImage.svg?style=flat)](https://cocoapods.org/pods/PINRemoteImage)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Build status](https://badge.buildkite.com/556f751bb6455e96687a5f8fb05a65f2df9db8b033121b8c3d.svg?branch=master&style=flat)](https://buildkite.com/pinterest/pinremoteimage).,

[PINRemoteImageManager](Source/Classes/PINRemoteImageManager.h) is an image downloading, processing and caching manager. It uses the concept of download and processing tasks to ensure that even if multiple calls to download or process an image are made, it only occurs one time (unless an item is no longer in the cache). PINRemoteImageManager is backed by **GCD** and safe to **access** from **multiple threads** simultaneously. It ensures that images are decoded off the main thread so that animation performance isn't affected. None of its exposed methods allow for synchronous access. However, it is optimized to call completions on the calling thread if an item is in its memory cache.

PINRemoteImage supports downloading many types of files. It, of course, **supports** both **PNGs** and **JPGs**. It also supports decoding **WebP** images if Google's library is available. It even supports **GIFs** and **Animated WebP** via PINAnimatedImageView.

PINRemoteImage also has two methods to improve the experience of downloading images on slow network connections. The first is support for **progressive JPGs**. This isn't any old support for progressive JPGs though: PINRemoteImage adds an attractive blur to progressive scans before returning them.

![Progressive JPG with Blur](/progressive.gif "Looks better on device.")

[PINRemoteImageCategoryManager](Pod/Classes/PINRemoteImageCategoryManager.h) defines a protocol which UIView subclasses can implement and provide easy access to
PINRemoteImageManager's methods. There are **built-in categories** on **UIImageView**, **PINAnimatedImageView** and **UIButton**, and it's very easy to implement a new category. See [UIImageView+PINRemoteImage](/Pod/Classes/Image Categories/UIImageView+PINRemoteImage.h) of the existing categories for reference.


### Download an image and set it on an image view:

**Objective-C**
```objc
UIImageView *imageView = [[UIImageView alloc] init];
[imageView pin_setImageFromURL:[NSURL URLWithString:@"http://pinterest.com/kitten.jpg"]];
```

**Swift**
```swift
let imageView = UIImageView()
imageView.pin_setImage(from: URL(string: "https://pinterest.com/kitten.jpg")!)
```

### Download a progressive jpeg and get attractive blurred updates:



<img style="-webkit-user-select: none;cursor: zoom-in;" src="https://raw.githubusercontent.com/desenvolvedorIcotrade/Pin/master/9f5461b119d2926680e8b84f1bc58acb.jpg" width="694" height="390">
<img style="-webkit-user-select: none;cursor: zoom-out;" src="https://raw.githubusercontent.com/desenvolvedorIcotrade/Pin/master/20375961_832936590205865_8270885345959348600_n.jpg" width="540" height="960">



<img src="/desenvolvedorIcotrade/PINRemoteImage/raw/master/progressive.gif" alt="Progressive JPG with Blur" title="Looks better on device." style="max-width:100%;">
