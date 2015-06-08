![screenshot](https://raw.githubusercontent.com/eface2face/iosrtc-apprtc/master/art/iosrtc-apprtc.jpg)


# iosrtc-apprtc

Google's [AppRTC](https://github.com/webrtc/apprtc) running in Cordova iOS with HTML5 and [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc).

This project takes the HTML5 version of the [AppRTC](https://apprtc.appspot.com/) applications and runs it in Cordova iOS (iPhone, iPad...) by using the [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc). 


## Building

Get the source code and add the Cordova iOS platform:

```bash
$ cordova platform add ios
```

Then install the *cordova-plugin-iosrtc* (or add it into your Cordova app's `config.xml`):

```bash
$ cordova plugin add com.eface2face.iosrtc
```

And run as usual.


## Usage

Once running, enter the same room as one already created via web browser at https://apprtc.appspot.com/, and enjoy!


## Changes in the original AppRTC HTML5 code

There are minor changes in the original HTML, JavaScript and CSS in order to make it work as a Cordova application. Those changes are:

* `js/apprtc.debug.js` and `js/appwindow.js` are loaded once Cordova's `ondeviceready` event is fired. This is needed since `js/apprtc.debug.js` relies on existing `window.webkitRTCPeerConnection` and `navigator.webkitGetUserMedia` which are not set by the *cordova-plugin-iosrtc* until `ondeviceready` fires.

* `webrtcDetectedVersion` global variable is hardcoded to `43` (AppRTC JavaScript code expects browser to be Chrome or Chromium, and fails otherwise).

* Given that the video stream is not directly attached to the `<video>` element (the *cordova-plugin-iosrtc* places a native `UIView` on top of it) the video `readyState` property is always 0, so the function `waitForRemoteVideo_` has been modified not to rely on `remoteVideo_.readyState >= 2`.

* In order to correctly place video views (iOS native `UIView` elements) the plugin `refreshVideos()` is called when the local or video video is set (this is because the CSS video elements use "transition" effects that modify their position and size during 1 second).

* A new CSS file `css/main_overrides.css` changes the properties of video elements. For example, it sets `opacity: 0.85` in `#local-video` and `#remote-video` so HTML call controls are shown even below the native `UIView` elements rendering the local and remote video.
