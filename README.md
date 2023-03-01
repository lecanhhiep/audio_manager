# audio_manager
[![pub package](https://img.shields.io/pub/v/audio_manager.svg)](https://pub.dartlang.org/packages/audio_manager)

A flutter plugin for music playback, including notification handling.
> This plugin is developed for iOS based on AVPlayer, while android is based on mediaplayer

<img src="https://raw.githubusercontent.com/jeromexiong/audio_manager/master/screenshots/android.png" height="300" alt="The example app running in Android"><img src="https://raw.githubusercontent.com/jeromexiong/audio_manager/master/screenshots/android2.png" height="300" alt="The example app running in Android"><img src="https://raw.githubusercontent.com/jeromexiong/audio_manager/master/screenshots/iOS.png" height="300" alt="The example app running in iOS"><img src="https://raw.githubusercontent.com/jeromexiong/audio_manager/master/screenshots/iOS2.jpeg" height="300" alt="The example app running in iOS">

## iOS
Add the following permissions in the `info.plist` file
```xml
	<key>UIBackgroundModes</key>
	<array>
		<string>audio</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSAllowsArbitraryLoads</key>
		<true/>
	</dict>
```
- ⚠️ Some methods are invalid in the simulator, please use the real machine

## Android
Since `Android9.0 (API 28)`, the application disables HTTP plaintext requests by default. To allow requests, add `android:usesCleartextTraffic="true"` in `AndroidManifest.xml`
```xml
<application
	...
	android:usesCleartextTraffic="true"
	...
>
```
- ⚠️ Android minimum supported version 23 `(app/build.gradle -> minSdkVersion: 23)`
- ⚠️ Android minimum supported Gradle version is 5.4.1 `(gradle-wrapper.properties -> gradle-5.4.1-all.zip)`

## How to use?
The `audio_manager` plugin is developed in singleton mode. You only need to get`AudioManager.instance` in the method to quickly start using it.

## Quick start
you can use local `assets`, `directory file` or `network` resources

```dart
// Initial playback. Preloaded playback information
AudioManager.instance
	.start(
		"assets/audio.mp3",
		// "network format resource"
		// "local resource (file://${file.path})"
		"title",
		desc: "desc",
		// cover: "network cover image resource"
		cover: "assets/ic_launcher.png")
	.then((err) {
	print(err);
});

// Play or pause; that is, pause if currently playing, otherwise play
AudioManager.instance.playOrPause()

// events callback
AudioManager.instance.onEvents((events, args) {
	print("$events, $args");
}
```
