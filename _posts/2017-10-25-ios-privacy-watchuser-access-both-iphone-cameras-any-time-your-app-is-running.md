---
layout: post
title: 'iOS Privacy: watch.user - Access both iPhone cameras any time your app is running'
categories: []
tags:
- ios
- privacy
- phishing
- camera
- video
status: publish
type: post
published: true
meta: {}
---

<div class="press">
  <a href="https://lifehacker.com/how-to-stop-ios-apps-from-secretly-spying-through-your-1819877630">
    <img src="/assets/privacy/Lifehacker.png">
  </a>
  <a href="https://9to5mac.com/2017/10/26/ios-camera-permissions-abuse/">
    <img src="/assets/privacy/9to5.png">
  </a>
  <a href="https://gizmodo.com/developer-shows-how-iphone-apps-can-theoretically-spy-o-1819874714">
    <img src="/assets/privacy/Gizmodo.png">
  </a>
  <a href="http://www.telegraph.co.uk/technology/2017/10/26/warning-iphone-apps-can-silently-turn-cameras-time/">
    <img src="/assets/privacy/Telegraph.png">
  </a>
  <a href="http://www.dailymail.co.uk/sciencetech/article-5020769/iPhone-apps-silently-turn-camera.html">
    <img src="/assets/privacy/DailyMail.jpg">
  </a>
  <a href="https://thenextweb.com/apple/2017/10/26/iphone-camera-permissions-google-ios/">
    <img src="/assets/privacy/TheNextWeb.png">
  </a>
  <a href="https://www.macrumors.com/2017/10/26/developer-warns-iphone-camera/">
    <img src="/assets/privacy/MacRumors.png">
  </a>
  <a href="https://motherboard.vice.com/en_us/article/mb3ezy/iphone-apps-camera-permission-pictures-videos-without-you-noticing">
    <img src="/assets/privacy/Motherboard.svg">
  </a>
  <a href="https://www.unilad.co.uk/featured/creepy-apple-loophole-seriously-infringes-on-your-privacy/">
    <img src="/assets/privacy/Unilad.jpg">
  </a>
  <a href="https://www.theregister.co.uk/2017/10/25/ios_apps_camera_spying/">
    <img src="/assets/privacy/TheRegister.jpg">
  </a>
  <a href="https://www.foxnews.com/tech/iphone-apps-with-access-to-your-camera-can-secretly-spy-on-you">
    <img src="/assets/privacy/FoxNews.png">
  </a>
</div>

---

**Update 2020-06-22** [Apple has fixed this issue with iOS 14](https://twitter.com/KrauseFx/status/1275128155561484288)

# Facts

Once you grant an app access to your camera, it can

- access both the front and the back camera
- record you at any time the app is in the foreground
- take pictures and videos without telling you
- upload the pictures/videos it takes immediately
- run real-time face recognition to detect facial features or expressions

Have you ever used a social media app while using the bathroom? 🚽

All without indicating that your phone is recording you and your surrounding, no LEDs, no light or any other kind of indication.

## Disclaimer

This project is a proof of concept and should not be used in production. The goal is to highlight a privacy loophole that can be abused by iOS apps.

## What can an iOS app do?

iOS users often grant camera access to an app soon after they download it (e.g. to add an avatar or send a photo). These apps, like a messaging app or any news-feed-based app, can easily track the users face, take pictures, or live stream the front and back camera, without the user's consent.

- Get full access to the front and back camera of an iPhone/iPad any time your app is running in the foreground
- Use the front and the back camera to know what your user is doing right now and where the user is located based on image data
- Upload random frames of the video stream to your web service, and run a proper face recognition software, which enables you to
  - Find existing photos of the person on the internet
  - Learn how the user looks like and create a 3d model of the user's face
- Live stream their camera onto the internet (e.g. while they sit on the toilet), with the recent innovation around faster internet connections, faster processors and more efficient video codecs it's hard to detect for the average user
- Estimate the mood of the user based on what you show in your app (e.g. news feed of your app)
- Detect if the user is on their phone alone, or watching together with a second person
- Recording stunning video material from bathrooms around the world, using both the front and the back camera, while the user scrolls through a social feed or plays a game
- Using the new built-in iOS 11 Vision framework, every developer can very easily parse facial features in real-time like the eyes, mouth, and the face frame

## How can I protect myself as a user?

There are only a few things you can do:

- The only real safe way to protect yourself is using camera covers: There is many different covers available, find one that looks nice for you, or use a sticky note ([for example](https://www.amazon.com/Original-Webcam-Cover-directly-Manufacturer/dp/B01LWS2X8I)).
- You can revoke camera access for all apps, always use the built-in camera app, and use the image picker of each app to select the photo (which will cause you to run into a problem I described with [detect.location](https://github.com/krausefx/detect.location)).
- To avoid this as well, the best way is to use Copy & Paste to paste the screenshot into your messaging application. If an app has no copy & paste support, you'll have to either expose your image library, or your camera.

It's interesting that many people cover their camera, [including Mark Zuckerberg](https://www.nytimes.com/2016/06/23/technology/personaltech/mark-zuckerberg-covers-his-laptop-camera-you-should-consider-it-too.html).

## Proposal

How can the root of the problem be fixed, so we don't have to use camera covers?

- Offer a way to grant temporary access to the camera (e.g. to take and share one picture with a friend on a messaging app), related to [detect.location](https://github.com/krausefx/detect.location).
- Show an icon in the status bar that the camera is active, and force the status bar to be visible whenever an app accesses the camera
- Add an LED to the iPhone's camera (both sides) that can't be worked around by sandboxed apps, which is the elegant solution that the MacBook uses

I reported the issue to Apple with [rdar://35116272](https://openradar.appspot.com/radar?id=5007947352506368).

<div class="video" style="width: 250px; float: right;margin: 20px">
  <figure>
    <iframe width="240" height="400" src="//www.youtube.com/embed/GqWUaflPMh0" frameborder="0" allowfullscreen></iframe>
  </figure>
</div>

## About the demo

I didn't submit the demo to the App Store; however, you can very easily [clone the repo](https://github.com/KrauseFx/watch.user) and run it on your own device.

- You first have to take a picture that gets "posted" on the fake "social network" in the app
  - At this point, you've granted full access to both of your cameras every time the app is running
- You browse through a news feed
- After a bit of scrolling, you'll suddenly see pictures of yourself, taken a few seconds ago while you scrolled through the feed
- You realize you've been recorded the whole time, and with it, the app ran a face recognition algorithm to detect facial features.

You might say 

> Oh, obviously, I never grant camera permissions!

<img src="/assets/posts/watch-user-screenshot.jpg" style="width: 250px; float: right; border: 2px solid #BBB; margin: 10px" />

However, if you're using a messaging service, like Messenger, WhatsApp, Telegram or anything else, chances are high you already granted permission to access both your image library (see [detect.location](https://github.com/KrauseFx/detect.location)) and your camera. You can check which apps have access to your cameras and photo library by going to Settings > Privacy.

The full source code is available [on GitHub](https://github.com/KrauseFx/watch.user).

### How does the demo app get access to the camera?

Once you take and post one picture or video via a social network app, you grant full access to the camera, and any time the app is running, the app can use the camera.

### What's the screenshot on the right

As part of iOS 11, there is now an easy to use Vision framework, that allows developers to easily track faces. The screenshot shows that it's possible to get some basic emotions right, so I wrote a very basic mapping of a user's face to the corresponding emoji as a proof of concept. You can see the highlighted facial features, and the detected emoji at the bottom.

## Similar projects I've worked on 

I published more posts on how to access the camera, the user's location data, their Mac screen and their iCloud password, check out [krausefx.com/privacy](/privacy) for more.

---

Special thanks to [Soroush](https://twitter.com/khanlou), who came up with the initial idea for this write-up.

<h3 style="text-align: center; font-size: 40px; margin-top: 40px">
  <a href="https://github.com/KrauseFx/watch.user" target="_blank" style="text-decoration: underline;">
    Open on GitHub
  </a>
</h3>
