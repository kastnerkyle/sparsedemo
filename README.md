Android NDK bare bones
======================

Android NDK build from command line is not very well documented in one place so
I wrote this project skeleton and these quick building instructions.
So this is how you build NDK projects from scratch on the command line without
having to use Eclipse or other obstacles or having to jump between Android SDK
and NDK documentation.

0.  Install both, Android SDK and NDK. Make sure "android", "adb" and
    "ndk-build" are in your $PATH.

        $ export NDK=/path/to/android/ndk
        $ export ANDROID_SDK=/path/to/android/sdk
        $ export PATH=$NDK:$ANDROID_SDK/tools:$ANDROID_SDK/platform-tools:$PATH

1.  Figure out what target to build for

        $ android list target

2.  After touching AndroidManifest.xml, update the project

        $ android update project --name NdkSkeleton --path . --target android-16 --subprojects

3.  Build native code

        $ ndk-build NDK_DEBUG=1

4.  Create apk package signed with debug key.

        $ ant debug

5.  Install on device

        $ adb install -r bin/NdkSkeleton-debug.apk

6.  Launch app using adb.
    Or launch it clicking the app icon on the device.

        $ adb shell am start -a android.intent.action.MAIN -n foo.bar.NdkSkeleton/android.app.NativeActivity
