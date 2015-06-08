# iosrtc-apprtc

Google's [apprtc](https://github.com/webrtc/apprtc) app running on Cordova iOS with [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc).

This project takes the HTML5 version of the [apprtc](https://apprtc.appspot.com/) applications and runs it in Cordova iOS (iPhone, iPad...) by using the [cordova-plugin-iosrtc](https://github.com/eface2face/cordova-plugin-iosrtc). There are minor changes in the original HTML, JavaScript and CSS in order to make it work as a Cordova application.


## Building

Get the source code and add the Cordova iOS platform:

```bash
$ cordova platform add ios
```

Then install the *cordova-plugin-iosrtc*:

```bash
$ cordova plugin add com.eface2face.iosrtc
```

And run as usual.


## Usage

Once running, enter the same room as one already created via web browser at https://apprtc.appspot.com/, and enjoy!
