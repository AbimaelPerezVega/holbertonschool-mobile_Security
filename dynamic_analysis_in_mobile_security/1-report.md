# Challenge 1: Hooking Native Functions in Android

## Objective
Intercept and analyze native code in the Android application using Frida to extract a decrypted flag hidden within the native function `getSecretMessage`.

## Tools Used
- Frida
- ADB
- Objection
- Android Studio
- APKTool
- JADX

## Step-by-Step Process

### 1. Setup & App Behavior Analysis
- Installed `Apk_task1` on an emulator.
- Explored the user interface – the app had no obvious flag or output.
- Used `adb logcat` to view logs, nothing significant was output.

### 2. Identifying the Native Library
- Decompiled the APK using `APKTool` and `jadx`.
- Located native library: `libnative-lib.so`.

### 3. Listing Exported Functions
- Ran:
  ```bash
  frida -U -n com.example.apk_task1 -e 'Module.enumerateExportsSync("libnative-lib.so").forEach(e => console.log(e.name))'
