---
layout: post
title:  "After Effects Animations | Lottie in IOS"
date:   2019-11-14 07:21:00 -0400
categories: IOS, Swift, Lottie
---

# Resources:<br />
* IOS documentation for Lottie: <a href="https://airbnb.io/lottie/#/ios" target="_blank">Airbnb Lottie Documentation</a>
* A good resource for finding lottie animations and testing/saving your files: <a href="https://lottiefiles.com/" target="_blank">Lottie Files</a>
    * Preview files <a href="https://lottiefiles.com/preview" target="_blank">here</a>
    * Find animations <a href="https://lottiefiles.com/featured" target="_blank">here</a>

In order to create an animation in an IOS project using Lottie you need to first have an After Effects animation file. Create a simple AE text animation with opacity and two keyframes. One with 0% opacity at the biggining and one with 100% opacity at the end. When that is complete go to Window->Extensions->Bodymovin. When the popup window appears, you will want to specify the destination folder of your animation json files. Make sure to click the "selected" radio button and then click "Render". This will output a json file in the directory you specified. After that, put your json file in your ios project and it is ready to be refenced in code. 



# SWIFT Code for Animation
Create an view in your view controller and link the IBOutlet
```swift
@IBOutlet weak var lottieView: UIView!
```
Next create an animation view
```swift
let animationView = AnimationView()
```
From there you are now able to call the animation code using the following as a guide. "logo-data" is the name of the json file output by After Effects
```swift
animationView.animation = Animation.named("logo-data")
animationView.frame.size = lottieView.frame.size
animationView.contentMode = .scaleAspectFill
    
lottieView.addSubview(animationView)

animationView.play { (finished) in
    \\ADD COMPLETION CODE HERE
}
```
