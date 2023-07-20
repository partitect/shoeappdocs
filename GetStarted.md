##### Get Started

-   Flutter & Dart [SDK](https://flutter.dev/docs/get-started/install) (We have used Flutter version 2.10)
-   Anyone IDE [Android Studio](https://developer.android.com/studio) (Recommended), [ Visual Studio Code](https://code.visualstudio.com/) or [ IntelliJ IDEA](https://www.jetbrains.com/idea/)

-   To edit this project you must have Flutter and Dart installed and configured successfully on your computer.
-   Set up your editor -- Install the[ Flutter and Dart plugins](https://flutter.dev/docs/get-started/editor?tab=androidstudio).
-   If you have got Android SDK installed and configured, to install Flutter you only need to:
    -   Download Flutter SDK from official website and extract it.
    -   Add path to previously extracted SDK to your PATH variable
    -   Run flutter doctor tool to check if everything is configured correctly.
    -   All above steps are mentioned here: <https://flutter.dev/docs/get-started/install/>

#### Setup in different Systems

##### Windows

-   Download Android Studio -- <https://developer.android.com/studio/>
-   Get the Flutter SDK -- <https://flutter.dev/docs/get-started/install>
-   Learn more about Android Studio -- <https://developer.android.com/studio/intro/>

##### macOS

-   Download Android Studio -- <https://developer.android.com/studio/>
-   Download Xcode -- <https://apps.apple.com/us/app/xcode/id497799835?mt=12>
-   Get the Flutter SDK -- <https://flutter.dev/docs/get-started/install>
-   Learn more about Android Studio -- <https://developer.android.com/studio/intro/>

##### Linux

-   Download Android Studio -- <https://developer.android.com/studio>
-   Get the Flutter SDK -- <https://flutter.dev/docs/get-started/install/linux>
-   Learn more about Android Studio -- <https://developer.android.com/studio/intro/>

#### SDK Version

If you Shoe App your project then you need to change following changes.

##### Flutter (v2.10 or higher)

-   You need Flutter v2.10 or higher (Stable Channel). For this run following commands.
-   flutter channel master to switch master branch for flutter SDK.
-   flutter upgrade to upgrade flutter to latest stable release.

##### Android (SDK 20 or Higher)

-   You need Android API 20 or higher. For this follow some steps.
-   Open `/android/app/build.gradle`

```
defaultConfig {
    applicationId "YOUR_APPLICATION_ID"
    minSdkVersion 21   // Change here - 20 or higher
    targetSdkVersion 30
    versionCode flutterVersionCode.toInteger()
    versionName flutterVersionName
}
```

##### iOS (9.0 or Higher)

-   You need iOS Version 9.0 or higher. For this follow some steps and run these commands
-   Open `/ios/Flutter/AppFrameworkInfo.plist`

```
<dict>
  ...
  <key>MinimumOSVersion</key>
  <string>9.0</string>    // Change here - 9.0 or higher
</dict>
```

-   rm ios/Podfile to remove podfile.
-   flutter clean to clean old builds.
-   flutter run to run project again.