---
layout: post
title:  "First Look of Android Development from an iOS Developer"
date:   2015-09-09 16:00:00 +0800
categories: Android
---


As much as I love iOS programming, circumstances have forced me to get into Android development. I have to adjust not only in the programming language, but also in programming style or structure, as Android has a different perspective on how it sees its apps. I'm just getting started with Android, so my opinions here are based from what I have currently learned.

## Programming Language

The main difference between the two platforms is the programming language. Android uses Java programming language, which can be used for cross-platform development using Java's Java Virtual Machine or JVM. iOS uses Objective-C or Swift, which is exclusive for their platform. Although, Apple recently announced in WWDC 2015 that they will open source Swift and its compiler. This will allow developers to use and modify Swift to suit their needs, such as creating native apps for other platforms.

## App Architecture

Moreover, Android's app architecture is surprisingly different from Android. For Android, an app's screen is an Activity class, on the other hand, an iOS app's screen is a ViewController. An Activity is like an independent app for Android, such that it manages its own lifecycle (OnCreate, OnPause, etc.). While for iOS, a ViewController is simply an object, and its lifecycle is similar to that of any object, wherein the app's lifecycle is managed by the `AppDelegate`, a separate object. This makes it easier to pass data between screens in iOS, since you can simply use the ViewController's properties to get or pass data. However, in Android, you can only pass primitive types such as a `string` or convert an object to `Parcelable` using `Intent`s, an object that is used to transition between Activities.

One weird thing I saw for the lifecycle of an Android app is that when the device rotates, the "Activity" is destroyed, then recreated again just to re-layout the view and its subviews. This can be a waste of computing power since it may repeat tasks that have already been done.

## UI Construction

For iOS, Xcode's interface builder allows us to easily create UI by drag-and-drop, making developers generally ignore the source code behind the UI. However, Android's official IDEs, Android Studio or Eclipse with ADT, developers mostly use the source code for editing UI and the app's flow. Android's IDEs support drag-and-drop, but it may be limited such that it is faster to edit the source code. I may not be sure about this, but most online tutorials for Android seems to prove that developers usually manually edit the source code of the UI.

## Conclusion

So, that's the main differences I saw between the two platforms while only touching the surface of Android development. In my opinion, iOS development is a better platform to get started with. Although, I also see some good things in Android development, such as its focus on separating static strings to a separate resource file, or its `LinearLayout` and `RelativeLayout`, which makes it easy for creating simple user interfaces. But if I were to choose between iOS development and Android development, I would stay with iOS due to its faster development time, and its official development environment, Xcode, is a more mature and beginner-friendly, IDE.