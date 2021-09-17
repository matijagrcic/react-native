# Setup

```bash
brew update
brew install mas
brew cask install visual-studio-code
brew cask install android-studio

# android-sdk requires Java 8. You can install it with:
brew cask install adoptopenjdk8

brew cask install vysor

sudo chmod 755 android/gradlew
android/local.properties add sdk.dir = /Users/YourUserNAME/Library/Android/sdk
```

```bash
#.zshrc
export ANDROID_HOME=$HOME/Library/Android/sdk
export ANDROID_SDK_ROOT=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

## Xcode command line tools

```bash
xcode-select --install
xcode-select -s /Applications/Xcode.app
```

[Setup Mobile Development Environment](https://gist.github.com/ThePredators/064c46403290a6823e03be833a2a3c21)
[Setup Macbook M1 for Web and React Native development](https://amanhimself.dev/blog/setup-macbook-m1/)
[ARM-Wrestling Your iOS Simulator Builds](https://apontious.com/2020/08/23/arm-wrestling-your-ios-simulator-builds/)
[React Native 0.64.2 with Apple M1 and Xcode 12.5](https://github.com/aiba/react-native-m1/blob/main/README.md)

# React Native Doctor

```bash
npx react-native doctor
```

Common

- ✓ Node.js
- ✓ yarn
- ✓ Watchman - Used for watching changes in the filesystem when in development mode

Android

- ✓ JDK
- ✓ Android Studio - Required for building and installing your app on Android
- ✓ Android SDK - Required for building and installing your app on Android
- ✓ ANDROID_HOME

iOS

- ✓ Xcode - Required for building and installing your app on iOS
- ✓ CocoaPods - Required for installing iOS dependencies
- ✓ ios-deploy - Required for installing your app on a physical device with the CLI

> Android SDK Command-line Tools for react-native need the 29.0.2 so under `System Settings > Android SDK > SDK Tools `tab select them.

## Mac Switch the Control and Command Keys

- From the Apple menu, select System Preferences.
- Select Keyboard.
- Click the Modifier Keys… button.
- From the Command Key menu, select Control. This lets Mac OS X know that you’ll be using the control key as the primary modifier.
- From the Control Key menu, select Command. This lets Mac OS X know that you’ll be using the command key as the secondary modifier.
- Click OK.
- Close the System Preferences.

[How to Switch the Control and Command Keys](https://www.macinstruct.com/tutorials/how-to-switch-the-control-and-command-keys/)

## Mac User Folder and Library

`cmd-shift-h` in Finder.

The user Library has been hidden since Mountain Lion, to temporarily reveal it, in Finder, hold down the Option key (ALT) and select Library from the Go menu.

To display it always, select your Home folder (cmd-shift-h) and Show View Options (cmd-j). Check the box to show the Library.
