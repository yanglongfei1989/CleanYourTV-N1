# Build

## Toolchain

- JDK 17
- Android SDK 34
- Gradle wrapper included in `launcher/`

```powershell
cd launcher
$env:JAVA_HOME="C:\path\to\jdk17"
$env:ANDROID_HOME="C:\path\to\android-sdk"
$env:ANDROID_SDK_ROOT=$env:ANDROID_HOME
.\gradlew.bat :app:assembleRelease
```

The APK is written to `launcher/app/build/outputs/apk/release/`.

## N1 changes to review

- `launcher/app/src/main/java/com/gathin/tvhome/MainActivity.java`
- `launcher/app/src/main/res/layout/activity_main.xml`
- `launcher/app/src/main/res/values/config.xml`
- `launcher/app/build.gradle`
- `launcher/app/src/main/AndroidManifest.xml`

The HOME activity uses API 25-compatible dependencies and keeps Java desugaring enabled for
`java.time`.

## Signing

The checked-in build uses the local Android debug key only for sideload testing. Replace
`signingConfig` with a stable release key before publishing. N1 Remote must be signed with the
same certificate for the status Provider permission.

