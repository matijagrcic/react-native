### Run on specific device

```bash
react-native run-ios

react-native run-ios --device "John's iPhone"
```

In `package.json` add the following script

`"run-ios-on-device": "react-native run-ios --device"`

and call it like so

`yarn run run-ios-on-device "John’s iPhone"`

### Running on simulator

You can specify the device the simulator should run with the `--simulator` flag, followed by the device name as a string. The default is "iPhone X".

```bash
npx react-native run-ios --simulator="iPhone SE"
npx react-native run-ios --udid XXXX
```

```bash
xcrun simctl --list
run react-native run-ios --simulator="iPhone 4s"
```

[https://www.iosdev.recipes/simctl/](https://www.iosdev.recipes/simctl/)

If `simctl` isn't found do the following `xcode-select -s /Applications/Xcode.app`

### List devices

To list all the devices run the following

`xcrun xctrace list devices` or

`xcrun simctl list devices` or

`xcrun instruments -s devices`

### Deploying on real device

```bash
brew install ios-deploy or  npm install -g ios-deploy
react-native run-ios --device "John’s iPhone"
react-native run-ios --udid XXXX --configuration Release
```

### iOS see device logs

```bash
brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>
```

[libimobiledevice](https://libimobiledevice.org/)

> A cross-platform FOSS library written in C to communicate with iOS devices natively.

For Windows and Android [libimobiledevice-win32](https://github.com/libimobiledevice-win32/imobiledevice-net/releases)
