---
title: "Debug Xamarin.iOS via wi-fi"
slug: "debug-xamarin-ios-via-wi-fi"
draft: false
date: "2018-03-07T07:36:00Z"
categories:
  - "Software Development"
tags:
  - "Xamarin"
author: "Curia Damiano"
image: "img/Debug-wifi-Visual-Studio-2017.png"
---

Visual Studio 2017 v15.6 and Visual Studio for Mac 7.4 introduce the possibility to debug Xamarin.iOS applications via wi-fi.

As [per Apple documentation](https://help.apple.com/xcode/mac/9.0/index.html?localePath=en.lproj#/devbc48d1bad), this requires to have installed on the Mac Xcode 9+ and iOS 11+.

How to do it? There are just a few steps to follow:
* in Xcode, connect your iPhone. Then from Window | Devices and Simulators, select your device and check "Connect via network"
  ![Xcode-before-Connect](img/Xcode-before-Connect.png)
* after checking, there should be a "world" symbol next to the iPhone:
  ![Xcode-after-Connect](img/Xcode-after-Connect.png)

This is enough to debug in both Visual Studio 2017 (note: "Connected via network")
![Debug-wifi-Visual-Studio-2017](img/Debug-wifi-Visual-Studio-2017.png)

and Visual Studio for Mac (note the wi-fi symbol)
![Debug-wifi-Visual-Studio-for-Mac](img/Debug-wifi-Visual-Studio-for-Mac.png)
