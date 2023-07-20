Using packages
--------------

The following section describes how to use existing published packages.

### [](https://docs.flutter.dev/packages-and-plugins/using-packages#searching-for-packages)Searching for packages

Packages are published to [pub.dev](https://pub.dev/).

The [Flutter landing page](https://pub.dev/flutter) on pub.dev displays top packages that are compatible with Flutter (those that declare dependencies generally compatible with Flutter), and supports searching among all published packages.

The [Flutter Favorites](https://pub.dev/flutter/favorites) page on pub.dev lists the plugins and packages that have been identified as packages you should first consider using when writing your app. For more information on what it means to be a Flutter Favorite, see the [Flutter Favorites program](https://docs.flutter.dev/packages-and-plugins/favorites).

You can also browse the packages on pub.dev by filtering on [Android](https://pub.dev/packages?q=sdk%3Aflutter+platform%3Aandroid), [iOS](https://pub.dev/packages?q=sdk%3Aflutter+platform%3Aios), [web](https://pub.dev/packages?q=sdk%3Aflutter+platform%3Aweb), [Linux](https://docs.flutter.dev/packages-and-plugins/using-packages?q=sdk%3Aflutter+platform%3Alinux), [Windows](https://pub.dev/packages?q=sdk%3Aflutter+platform%3Awindows), [macOS](https://pub.dev/packages?q=sdk%3Aflutter+platform%3Amacos), or any combination thereof.

### [](https://docs.flutter.dev/packages-and-plugins/using-packages#adding-a-package-dependency-to-an-app)Adding a package dependency to an app

To add the package, `css_colors`, to an app:

1.  Depend on it
    -   Open the `pubspec.yaml` file located inside the app folder, and add `css_colors:` under `dependencies`.
2.  Install it
    -   From the terminal: Run `flutter pub get`.\
        OR
    -   From VS Code: Click Get Packages located in right side of the action ribbon at the top of `pubspec.yaml` indicated by the Download icon.
    -   From Android Studio/IntelliJ: Click Pub get in the action ribbon at the top of `pubspec.yaml`.
3.  Import it
    -   Add a corresponding `import` statement in the Dart code.
4.  Stop and restart the app, if necessary
    -   If the package brings platform-specific code (Kotlin/Java for Android, Swift/Objective-C for iOS), that code must be built into your app. Hot reload and hot restart only update the Dart code, so a full restart of the app might be required to avoid errors like `MissingPluginException` when using the package.

### [](https://docs.flutter.dev/packages-and-plugins/using-packages#adding-a-package-dependency-to-an-app-using-flutter-pub-add)Adding a package dependency to an app using `flutter pub add`

To add the package, `css_colors`, to an app:

1.  Issue the command while being inside the project directory
    -   `flutter pub add css_colors`
2.  Import it
    -   Add a corresponding `import` statement in the Dart code.
3.  Stop and restart the app, if necessary
    -   If the package brings platform-specific code (Kotlin/Java for Android, Swift/Objective-C for iOS), that code must be built into your app. Hot reload and hot restart only update the Dart code, so a full restart of the app might be required to avoid errors like `MissingPluginException` when using the package.

### [](https://docs.flutter.dev/packages-and-plugins/using-packages#removing-a-package-dependency-to-an-app-using-flutter-pub-remove)Removing a package dependency to an app using `flutter pub remove`

To remove the package, `css_colors`, to an app:

1.  Issue the command while being inside the project directory
    -   `flutter pub remove css_colors`

The [Installing tab](https://pub.dev/packages/css_colors/install), available on any package page on pub.dev, is a handy reference for these steps.

For a complete example, see the [css_colors example](https://docs.flutter.dev/packages-and-plugins/using-packages#css-example) below.

### [](https://docs.flutter.dev/packages-and-plugins/using-packages#conflict-resolution)Conflict resolution

Suppose you want to use `some_package` and `another_package` in an app, and both of these depend on `url_launcher`, but in different versions. That causes a potential conflict. The best way to avoid this is for package authors to use [version ranges](https://dart.dev/tools/pub/dependencies#version-constraints) rather than specific versions when specifying dependencies.

content_copy

```
dependencies:
  url_launcher: ^5.4.0    # Good, any version >= 5.4.0 but < 6.0.0
  image_picker: '5.4.3'   # Not so good, only version 5.4.3 works.

```

If `some_package` declares the dependencies above and `another_package` declares a compatible `url_launcher` dependency like `'5.4.6'` or `^5.5.0`, pub resolves the issue automatically. Platform-specific dependencies on [Gradle modules](https://docs.gradle.org/current/userguide/declaring_dependencies.html) and/or [CocoaPods](https://guides.cocoapods.org/syntax/podspec.html#dependency) are solved in a similar way.

Even if `some_package` and `another_package` declare incompatible versions for `url_launcher`, they might actually use `url_launcher` in compatible ways. In this situation, the conflict can be resolved by adding a dependency override declaration to the app's `pubspec.yaml` file, forcing the use of a particular version.

For example, to force the use of `url_launcher` version `5.4.0`, make the following changes to the app's `pubspec.yaml` file:

content_copy

```
dependencies:
  some_package:
  another_package:
dependency_overrides:
  url_launcher: '5.4.0'

```

If the conflicting dependency is not itself a package, but an Android-specific library like `guava`, the dependency override declaration must be added to Gradle build logic instead.

To force the use of `guava` version `28.0`, make the following changes to the app's `android/build.gradle` file:

content_copy

```
configurations.all {
    resolutionStrategy {
        force 'com.google.guava:guava:28.0-android'
    }
}

```

CocoaPods doesn't currently offer dependency override functionality.