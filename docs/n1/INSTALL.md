# CleanYourTV N1 Installation

## Requirements

- Phicomm N1 with Android 7.1 / API 25
- ADB enabled over USB or wireless debugging
- A launcher-independent recovery path such as USB ADB

Tested firmware: `N1_A0_V2.19_A00_0307_NS`.

## Install

```powershell
adb connect <N1-IP>:5555
adb install -r dist\CleanYourTV-N1-API25.apk
adb shell cmd package set-home-activity com.gathin.tvhome/.MainActivity
```

Open Home and verify:

- Dock remains at the bottom after reboot.
- The first dock card owns focus and the glass highlight is aligned.
- The Remote status card appears between the clock and Dock.
- If N1 Remote is installed, the QR code appears only after port `8088` is accepting connections.

## N1 Remote integration

Install the separately published N1 Pocket Remote with the same signing certificate. The launcher
requests:

```text
com.gathin.n1remote.permission.READ_STATUS
```

The permission has `protectionLevel="signature"`, so rebuilding either app with a different key
will hide the status card.

## Updating

Use `adb install -r` for both projects together. Build outputs use the Android debug key by
default; for a public release, use one stable private signing key and distribute the matching
APKs.

## Uninstall

```powershell
adb uninstall com.gathin.tvhome
adb shell cmd package set-home-activity com.phicomm.launcherush.debug/.Launcher
```

The exact stock launcher component can differ by firmware; list HOME handlers before changing it.

