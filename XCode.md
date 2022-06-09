#Xcode specifics

Remove the deployment target settings from all pods using iOS 8 or below, allowing them to simply inherit the project deployment target that you have specified at the top of your Podfile
`platform :ios, '10.`

```ruby
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      if config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'].to_f < 9.0
        config.build_settings.delete 'IPHONEOS_DEPLOYMENT_TARGET'
        config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '9.0'
      end
    end
  end
end
```

add `s.platform = :ios, "9.0"` to .podspec file

> Update the Deployment Target to 9.0. This can be updated by opening the `.xcworkspace` file, choose the `Pods.xcodeproj` on Xcode, and updating the iOS Deployment Target to 9.0 or later as depicted in the below image.

> You can't provide support for iOS 8.0 on Xcode 12 unless you import the support files.

# Deprecations

- The Build Settings editor no longer includes the Valid Architectures build setting (VALID_ARCHS), and its use is discouraged. Instead, there is a new Excluded Architectures build setting (EXCLUDED_ARCHS).
  If a project includes VALID_ARCHS, the setting is displayed in the User-Defined section of the Build Settings editor. (15145028)
- The legacy build system is deprecated, and will be removed in a future release. (62742902)
- Xcode now supports debugging apps and running tests on iOS devices running iOS 9.0 and above. (59561001)

[Xcode 12 Release Notes](https://developer.apple.com/documentation/xcode-release-notes/xcode-12-release-notes)

### Flipper

[https://github.com/facebook/react-native/issues/31480#issue-876308920](https://github.com/facebook/react-native/issues/31480#issue-876308920)

### CocoaPods

[CocoaPods](https://guides.cocoapods.org/using/getting-started.html)

> CocoaPods manages library dependencies for your Xcode projects.

```bash
sudo gem install cocoapods
sudo gem uninstall cocoapods
sudo gem install -n /usr/local/bin cocoapods

brew upgrade cocoapods
brew install cocoapods
gem which cocoapods
sudo gem install cocoapods --pre
```

# Clearing a specific pod

```bash
pod cache clean --all # will clean all pods
pod cache clean 'SomeName' --all # will remove all installed 'SomeName' pods
```

# Complete cleanup (pod reset)

```bash
rm -rf ~/Library/Caches/CocoaPods
rm -rf Pods
rm -rf ~/Library/Developer/Xcode/DerivedData/\*
pod deintegrate #https://guides.cocoapods.org/terminal/commands.html#pod_deintegrate
pod setup
pod install
```

### RVM

```bash
rm -rf ~/.rvm
sudo curl -L https://get.rvm.io | bash -s stable --ruby

rbenv install 2.7.3

//change ruby version globally using:
rbenv global 2.7.3
```

### mas-cli

[mas-cli](https://github.com/mas-cli/mas#mas-cli)

> A simple command line interface for the Mac App Store. Designed for scripting and automation.

#### iPhone Screenshot & Screen Recording

[https://support.apple.com/en-gb/guide/iphone/iphc872c0115/ios](https://support.apple.com/en-gb/guide/iphone/iphc872c0115/ios)

- Set simulator to physical size: Window > Physical Size
- Set High-Quality Graphics: Debug > Graphics Quality Override > High Quality

Make screenshots as follows:

- for iPhone 6.5" Display - 1242 x 2688(portrait): simulator iPhone 11 Pro Max
- for iPhone 5.5" Display - 1242 x 2208(portrait): simulator iPhone 8 Plus
- for iPad Pro (3rd and 2nd generation) 12.9" Display - 2048 x 2732(portrait): simulator iPad Pro (12.9-inch) (3rd generation)

```bash
xcrun simctl io --help
xcrun simctl io booted screenshot <filename>.<file extension>
xcrun simctl io booted recordVideo <filename>.<file extension>
```

[iOS App Screenshots and Video Previews for App Store Connect](https://reefwing.medium.com/ios-app-screenshots-and-previews-for-itunes-connect-a5813bb1c47c)
[Screenshot specifications](https://help.apple.com/app-store-connect/#/devd274dd925)

### Builds

To list all targets, build configurations, and schemes used in your project, run the following

```bash
xcrun xcodebuild -list -project "./SomeApp.xcodeproj"
```

```bash
# see what's building
xcrun xcodebuild -showBuildSettings -scheme "Some" -project "./SomeApp.xcodeproj"
```

# Debugging

When your device is connected to your computer with a cable and you Build + Run your app, your device will try to debug.
Debugging is only permitted for Development profiles.

-If you build + run with a Development Profile + Development Signing Code, everything will be OK
Shake your iOS device and Reload

-If you build + run with an AppStore Distribution profile + Distribution Signing Code, the app will not even reach your device. This build is only for uploading to AppStore

-If you build + run with an AdHoc Distribution profile + Distribution Signing Code, you'll get the "failed to get the task for process..." error, but the app will get installed in your device.
Unplug the device and run the app from your device. It's running in distribution environment.

```bash
fastlane run register_device udid:"" name:""
match development --force_for_new_devices
match adhoc --force_for_new_devices
```

```ruby
 lane :register_a_device do
    register_devices(
      devices: {
        "name": "device UDID",
        "name": "device UDID",
      })
    refresh_profiles
  end

  lane :refresh_profiles do
    match(
      type: "development",
      force: true)
    match(
      type: "adhoc",
      force: true)
  end
```

```ruby
lane :add_device do
      device_name = prompt(text: "Enter the device name: ")
      device_udid = prompt(text: "Enter the device UDID: ")
      device_hash = {}
      device_hash[device_name] = device_udid
      register_devices(
        devices: device_hash
      )
    refresh_profiles
  end

  # A helper lane for refreshing provisioning profiles.
  lane :refresh_profiles do
    match(
      force_for_new_devices: true
   )
  end

```

> When you do _force_ or _force_for_new_devices_ it updates the existing profile

# Install XCode command line tools

```bash
xcode-select --install
xcode-select -p

# check path
xcode-select --print-path

# select default version of Xcode
sudo xcode-select -switch <path/to/>Xcode.app
```

[Building from the Command Line with Xcode FAQ](https://developer.apple.com/library/archive/technotes/tn2339/_index.html)

# Xcode not recognizing a connected device

- Quit Xcode
- Disconnect the device
- In a terminal window, type: `sudo pkill usbmuxd` (it will be restarted again automatically)
- Start Xcode
- Connect the device

# Debug logs

> Supports both USB or WIFI

```bash
brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid> | grep com.app.name
```

# Debug WebView

- Open Safari Preferences -> "Advanced" tab -> enable checkbox "Show Develop menu in menu bar"
- Start app with React Native WebView in iOS simulator or iOS device
- Safari -> Develop -> [device name] -> [app name] -> [url - title]
- You can now debug the WebView contents just as you would on the web

[Debugging WebView Contents](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Debugging.md#debugging-webview-contents)

# ProvisionQL - Quick Look for ipa & provision

[ealeksandrov/ProvisionQL](https://github.com/ealeksandrov/ProvisionQL)

> Inspired by a number of existing alternatives, the goal of this project is to provide clean, reliable, current and open source Quick Look plugin for iOS & macOS developers.
