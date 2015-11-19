![screenshot](https://raw.githubusercontent.com/eface2face/iOSRTCApp/master/art/photo1.jpg)

*NOTE:* This project is not being actively maintained and it may not work with the latest version of the [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc) or the latest server side code of the Google's AppRTC.


# iOSRTCApp

Google's [AppRTC](https://apprtc.appspot.com/) adapted to [Cordova](http://cordova.apache.org/) iOS with pure HTML5/JavaScript and [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc).

This project takes the [HTML5 version](https://github.com/webrtc/apprtc/tree/master/src/web_app) of the *AppRTC* application and runs it in Cordova iOS (iPhone, iPad...) by using the [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc) to provide the [WebRTC W3C JavaScript APIs](http://www.w3.org/TR/webrtc/).


## Building & usage

- Get the source code:
```bash
$ git clone https://github.com/eface2face/iOSRTCApp
$ cd iOSRTCApp
```
- Install NPM dependencies:
```bash
$ npm install
```
- Add both platforms. All the needed plugins are installed automatically because of being included in the "config.xml" file:
```bash
$ cordova platform add ios android
```
- Run as usual:
```bash
$ cordova run android --device
$ cordova run ios --device
```
- Once running, enter the same room as one already created via web browser at https://apprtc.appspot.com/, and enjoy!


## Changes to the original AppRTC HTML5 code

There are minor changes in the original HTML, JavaScript and CSS in order to make it work as a Cordova application. Those changes are:

- `js/apprtc.debug.js` and `js/appwindow.js` are loaded once Cordova's `ondeviceready` event is fired. This is needed since `js/apprtc.debug.js` relies on existing `window.webkitRTCPeerConnection` and `navigator.webkitGetUserMedia` which are not set by the *cordova-plugin-iosrtc* until `ondeviceready` fires.
- `webrtcDetectedVersion` global variable is hardcoded to `43` (AppRTC JavaScript code expects browser to be Chrome or Chromium, and fails otherwise).
- In order to correctly place video views (iOS native `UIView` elements) the plugin `refreshVideos()` function is called when the local or remote video is set (this is because the CSS video elements use "transition" effects that modify their position and size during 1 second).
- A new CSS file `css/main_overrides.css` changes the properties of video elements. For example, it sets `opacity: 0.85` in `#local-video` and `#remote-video` so HTML call controls are shown even below the native `UIView` elements rendering the local and remote video.


## Author

*AppRTC* code is owned by Google as stated in the original [LICENSE](LICENSE.md) file.

Changes to the original *AppRTC* HTML5 source code (to become a Cordova iOS application) are written by Iñaki Baz Castillo at [eFace2Face, inc](https://eface2face.com).
