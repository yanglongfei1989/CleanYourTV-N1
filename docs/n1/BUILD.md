# 构建说明

## 工具链

- JDK 17
- Android SDK 34
- `launcher/` 中自带的 Gradle Wrapper

```powershell
cd launcher
$env:JAVA_HOME="C:\path\to\jdk17"
$env:ANDROID_HOME="C:\path\to\android-sdk"
$env:ANDROID_SDK_ROOT=$env:ANDROID_HOME
.\gradlew.bat :app:assembleRelease
```

APK 输出到 `launcher/app/build/outputs/apk/release/`。

## N1 主要修改文件

- `launcher/app/src/main/java/com/gathin/tvhome/MainActivity.java`
- `launcher/app/src/main/res/layout/activity_main.xml`
- `launcher/app/src/main/res/values/config.xml`
- `launcher/app/build.gradle`
- `launcher/app/src/main/AndroidManifest.xml`

HOME Activity 使用兼容 API 25 的依赖，并保留 `java.time` 的 Java Desugaring。

## 签名

仓库中的构建仅供本地侧载测试，使用 Android 调试密钥。公开发布前请替换 `signingConfig`。N1 Remote 必须使用同一证书签名，状态 Provider 权限才能生效。

