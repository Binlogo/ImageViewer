# ImageViewer

<a href="https://github.com/Carthage/Carthage"><img src="https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat"></a>
![](https://travis-ci.org/MailOnline/ImageViewer.svg?branch=master)

ImageViewer is a library that enables a user to visualize an image in fullscreen. Besides the typical pinch and double tap to zoom, we also provide a vertical swipe to dismiss. Finally, we try to mimic the displacement of the image from its current container into fullscreen, this feature being its main selling point. In our context, you can imagine an image as part of an article and when it's tapped, the image is animated into fullscreen.

![](Documentation/preview.gif)


#### Setup

With Carthage:

```
github "MailOnline/ImageViewer"
```

#### Usage


```swift

let imageProvider: ImageProvider = ... 

let buttonConfiguration = ButtonStateAssets(normalImage:UIImage(named: "normalImage"), highlightedImage:UIImage(named: "highlightedImage"))
let configuration = ImageViewerConfiguration(imageSize: size, closeButtonAssets: buttonConfiguration)

let imageViewer = ImageViewer(imageProvider: imageProvider, configuration: configuration, displacedView: displacedView)

imageViewer.show()
```

* `imageProvier`: An object that is able to provide an image via a callback `UIImage? -> Void`.
* `configuration`: Contains information about the assets that will be used for the close button and the image to be displayed's size.
* `displacedView`: The view that is about to be displayed in fullscreen. 

#### Roadmap 

- [X] Setup Travis
- [ ] Clean up internal logic (refactoring mostly)
- [X] Remove the XIB file and create the UI with code
- Investigation
 - [ ] Investigate the usage of custom transitions
 - [ ] Investigate a more idiomatic way of dealing with the orientation changes
- [ ] UI Testing
- [ ] Expand the ImageViewer to a Gallery

#### Caveats

Because `ImageViewer` was created with a given configuration in mind, it might be limiting factor for certain apps:

* Currently the library will only behave correctly in apps that have rotation disabled (only Portrait). Since we are applying transformations and listening for `UIDeviceOrientationDidChangeNotification`. We have a couple of ideas on how to solve this problem and provide a more predictable behaviour. Given all this,  you shouldn't use for an iPad app.
* `ImageViewer` is currently a `UIViewController` subclass, we are considering making it a `UIView`, as we find the later lifecycle more reliable. We are adding `ImageViewer`'s root view to the `UIWindow`'s `subViews` and itself as a `childViewController` of the `window.rootViewController`. We are still looking into a way of making this part a bit more idiomatic, while maintaining the great fullscreen look. 
* We are seeing some issues with the animations due to different aspect ratio between the `displacedView` and the fullscreen `UIImageView`. We aren't sure if it's worth to fix this, as we don't run into this problem.


## License
ImageViewer is licensed under the MIT License, Version 2.0. [View the license file](LICENSE)

Copyright (c) 2015 MailOnline
