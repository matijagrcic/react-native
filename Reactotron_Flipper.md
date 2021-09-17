Download [Flipper](https://fbflipper.com/)

Download [watchman](https://github.com/facebook/watchman/releases) and add the `\bin` to the `PATH`
the install `openssl`

```bash
choco install openssl
```

Download [Reactotron](https://github.com/infinitered/reactotron/releases)

```bash
npm install react-native-flipper
npm install --save-dev reactotron-react-native
npm install @react-native-community/async-storage
```

```js
//ReactotronConfig.js

import Reactotron from "reactotron-react-native";
import ReactotronFlipper from "reactotron-react-native/dist/flipper";
import AsyncStorage from "@react-native-community/async-storage";

Reactotron.setAsyncStorageHandler(AsyncStorage)
  .configure({
    name: "AppName",
    createSocket: (p) => new ReactotronFlipper(p),
  })
  .useReactNative()
  .connect();
```

In `App.tsx` add

```js
if (__DEV__) {
  import("./ReactotronConfig").then(() => {
    console.log("Reactotron Configured");
  });
}
```

In `android/app/build.gradle` add

```js
defaultConfig {
    multiDexEnabled true
}
```

In `AndroidManifest.xml` add

```xml
<activity android:name="com.facebook.flipper.android.diagnostics.FlipperDiagnosticActivity"
        android:exported="true"/>
```

Set up port forwarding

```bash
adb reverse tcp:9090 tcp:9090
```

Useful commands

```bash
adb reverse --list
adb kill-server
adb start-server
adb forward --remove-all
```

```ps
Get-Process -ID (Get-NetTCPConnection -LocalPort 8088).OwningProcess
```

```bash
npx react-devtools
```

## Talks

_Flipper: The Extensible DevTool Platform for React Native - Michel Weststrate aka @mweststrate_

[![Flipper: The Extensible DevTool Platform for React Native - Michel Weststrate aka @mweststrate](https://img.youtube.com/vi/WltZTn3ODW4/0.jpg)](https://www.youtube.com/watch?v=WltZTn3ODW4)

_Flipper: The Extensible DevTool Platform for React Native - Michel Weststrate_

[![Flipper: The Extensible DevTool Platform for React Native - Michel Weststrate](https://img.youtube.com/vi/bI1VEXVzNXs/0.jpg)](https://www.youtube.com/watch?v=bI1VEXVzNXs)

## Issues

[https://github.com/facebook/react-native/issues/31179](https://github.com/facebook/react-native/issues/31179)
[Xcode 12.5 troubleshooting guide (RN 0.61/0.62/0.63/0.64)](https://github.com/facebook/react-native/issues/31480)
