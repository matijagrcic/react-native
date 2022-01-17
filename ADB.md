> Android Debug Bridge command line tool adb

Install [options]
<PATH> Installs a package (specified by <PATH>) to the system.

Options:

- -l: Install the package with forward lock.
- -r: Reinstall an exisiting app, keeping its data.
- -t: Allow test APKs to be installed.
- -i <INSTALLER_PACKAGE_NAME>: Specify the installer package name.
- -s: Install package on the shared mass storage (such as sdcard).
- -f: Install package on the internal system memory.
- -d: Allow version code downgrade.

[Ref](https://developer.android.com/studio/command-line/adb)

> ADB over WIFI

On some devices you can find in dev options the _Enable ADB over network_ setting then do `adb connect <DEVICE_IP_ADDRESS>:5555`

- Connect the device via USB and make sure debugging is working
- `adb tcpip 5555`. This makes the device to start listening for connections on port 5555
- Look up the device IP address with `adb shell netcfg` or `adb shell ifconfig` with 6.0 and higher;+
- You can disconnect the USB now
- `adb connect <DEVICE_IP_ADDRESS>:5555` - this connects to the server we set up on the device on step 2
- to go back to USB execute `adb usb`

# Bundletool

> Extract apks from aab file and install it to a device

```bash
brew install bundletool
bundletool build-apks --bundle=./app.aab --output=./app.apks
```

[bundletool](https://developer.android.com/studio/command-line/bundletool)
[google/bundletool](https://github.com/google/bundletool/releases)

[Bundletool for Fastlane](https://github.com/MartinGonzalez/fastlane-plugin-bundletool)

```bash
bundletool(
  ks_path: keystore_path,
  ks_password: keystore_password,
  ks_key_alias: keystore_alias,
  ks_key_alias_password: keystore_alias_password,
  bundletool_version: '1.8.2',
  aab_path: aab_path,
  apk_output_path: apk_output_path,
  verbose: true
)
```

# Debug APK

```bash
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
cd android && ./gradlew assembleDebug
```

The APK will be stored in `/android/app/build/outputs/apk/debug/app-debug.apk`
