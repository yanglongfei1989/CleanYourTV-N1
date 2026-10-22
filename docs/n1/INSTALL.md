# CleanYourTV N1 安装说明

## 环境要求

- 斐讯 N1，Android 7.1 / API 25
- 已开启 USB 调试或无线调试
- 保留不依赖当前桌面的恢复路径，例如 USB ADB

实测固件：`N1_A0_V2.19_A00_0307_NS`。

## 安装

```powershell
adb connect <N1-IP>:5555
adb install -r dist\CleanYourTV-N1-API25.apk
adb shell cmd package set-home-activity com.gathin.tvhome/.MainActivity
```

打开首页并确认：

- 重启后 Dock 仍固定在底部。
- 第一张 Dock 卡片获得焦点，玻璃高亮框位置正确。
- 遥控状态卡显示在时钟和 Dock 之间。
- 安装 N1 Remote 后，只有在 `8088` 开始接受连接时才会显示二维码。

## N1 Remote 集成

安装使用同一签名证书的 N1 Pocket Remote。桌面声明以下权限：

```text
com.gathin.n1remote.permission.READ_STATUS
```

该权限的 `protectionLevel="signature"`。任一 APK 使用不同签名重新构建时，状态卡会隐藏。

## 更新

两个项目应同时使用 `adb install -r` 更新。当前构建产物默认使用 Android 调试密钥；公开发布时应改用稳定的私有签名密钥，并分发同一密钥签名的两个 APK。

## 卸载

```powershell
adb uninstall com.gathin.tvhome
adb shell cmd package set-home-activity com.phicomm.launcherush.debug/.Launcher
```

不同固件的原厂桌面组件可能不同，修改默认 Home 前应先查询所有 HOME Handler。

