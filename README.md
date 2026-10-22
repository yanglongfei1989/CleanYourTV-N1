# CleanYourTV N1

> [!IMPORTANT]
> **AI 构建声明：** 本 N1 衍生版由 AI 协助完成代码修改、界面设计、测试和文档。虽然已在真实斐讯 N1 上验证，使用前仍应自行审计源码、备份系统并保留恢复通道。

> [!NOTE]
> 本项目是 [Gathin23/cleanyourtv](https://github.com/Gathin23/cleanyourtv) 的非官方 N1 衍生版，不代表上游作者或官方发行。原始英文 README 保存在 [README.upstream.md](README.upstream.md)。

## 项目定位

CleanYourTV N1 面向斐讯 N1 和 Android TV 7.1 设备，在上游 CleanYourTV 桌面的基础上补充 API 25 兼容、开机焦点修复、手机遥控二维码集成和电视应用横幅。

实测环境：

- 斐讯 N1 `p230`
- 固件 `N1_A0_V2.19_A00_0307_NS`
- Android 7.1.2 / API 25
- 1920×1080@60

## 主要改进

- 冷启动后 Dock 稳定停在底部，第一张卡片获得焦点。
- 修复应用扫描较慢时网格抢占焦点、高亮框漂移的问题。
- 首页显示 N1 Pocket Remote 地址、动态 PIN 和服务状态。
- 通过同签名 `ContentProvider` 读取 PIN，不开放匿名状态接口。
- 服务上线后自动显示二维码；启动中和断网状态使用紧凑深色提示。
- Remote、AVBox、设置等应用使用持久 16:9 电视横幅。
- 横幅通过 `app_banners` 按包名映射，应用更新或重装后仍能保持。
- 支持明确设置 CleanYourTV 为默认首页。

![设置横幅](docs/n1/banner-settings.png)
![AVBox 横幅](docs/n1/banner-avbox.png)
![N1 Remote 横幅](docs/n1/banner-n1remote.png)

## 安装

```powershell
adb connect <N1-IP>:5555
adb install -r dist\CleanYourTV-N1-API25.apk
adb shell cmd package set-home-activity com.gathin.tvhome/.MainActivity
```

配套手机遥控项目：

<https://github.com/jimmieyangcsjs/N1-Pocket-Remote>

两个 APK 必须使用同一签名，首页才能读取遥控状态。

详细文档：

- [安装说明](docs/n1/INSTALL.md)
- [构建说明](docs/n1/BUILD.md)
- [遥控集成说明](docs/n1/INTEGRATION.md)
- [N1 中文介绍](README.N1.md)
- [AI 构建声明](AI-NOTICE.md)

## 构建

需要 JDK 17 和 Android SDK 34：

```powershell
cd launcher
$env:JAVA_HOME="C:\path\to\jdk17"
$env:ANDROID_HOME="C:\path\to\android-sdk"
$env:ANDROID_SDK_ROOT=$env:ANDROID_HOME
.\gradlew.bat :app:assembleRelease
```

## 性能与 4K

- 1080p60 连续焦点移动实测 912 帧、0 卡顿帧，95% 帧耗时约 6 ms。
- 当前电视 EDID 和固件最高只提供 1080p60，没有原生 4K UI 模式。
- 项目不强制 4K 自动降级，保留用户配置的动画、缩放和辉光。

## 开源归属

- 上游项目：<https://github.com/Gathin23/cleanyourtv>
- 上游许可证：MIT
- 本仓库保留上游许可证、版权声明、来源提交和第三方资源说明。
- 修改与归属详见 [NOTICE.md](NOTICE.md)。

本衍生版同样按 MIT License 分发。

![AI 辅助构建](https://img.shields.io/badge/build-AI%20%E8%BE%85%E5%8A%A9%E6%9E%84%E5%BB%BA-ff8a4c?labelColor=15181e)

