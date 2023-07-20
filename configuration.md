### Android Configuration

#### Open Android module in Android Studio

1.  Open Android Studio.
2.  Select Open an existing Android Studio Project.
3.  Open the android directory within your app.
4.  Wait until the project has been synced successfully. (This happens automatically once you open the project, but if it doesn't, select Sync Project with Gradle Files from the File menu).
5.  Now, click on Run button.

#### Change Application Name

1.  You must want to change your application name. This is how you can do. Follow the below step.
2.  Open `/android/app/src/main/AndroidManifest.xml` and specify your application name.

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application
        android:name="io.flutter.app.FlutterApplication"
        android:label="YOUR_APPLICATION_NAME"      // Change here
        android:icon="@mipmap/ic_launcher">
        <activity...
```

#### Change Application ID

1.  Follow the below steps to change you Application ID.
2.  Open `/android/app/build.gradle`

```
    defaultConfig {
        applicationId "YOUR_APPLICATION_ID"      // Change here - com.company_name.product_name (Like com.example.shoeapp)
        minSdkVersion 21
        targetSdkVersion 30
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
```

#### Change Application Icon

1.  See [ How to generate an application icon?](https://romannurik.github.io/AndroidAssetStudio/icons-launcher.html)
2.  Browse your image and click on Download icon. After successfully generated, replace all icons in respective folders:
3.  Change Splash Screen Style
4.  Change Splash Screen Style (For Android API above 21)
5.  Change Splash Screen Image
6.  Change Application Icon

-   `/mipmap-hdpi   ` in `/android/app/src/main/res/` folder
-   `/mipmap-mdpi   ` in `/android/app/src/main/res/` folder
-   `/mipmap-xhdpi  ` in `/android/app/src/main/res/` folder
-   `/mipmap-xxhdpi ` in `/android/app/src/main/res/` folder
-   `/mipmap-xxxhdpi` in `/android/app/src/main/res/` folder

#### Important:

If you don't know how to change logo from Android Manifest (/android/app/src/main/AndroidManifest.xml), Then icon name must be logo.png.