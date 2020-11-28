## Header Height

```js
import { useHeaderHeight } from "@react-navigation/stack";

const headerHeight = useHeaderHeight();
```

```js
import { HeaderHeightContext } from '@react-navigation/stack';

<HeaderHeightContext.Consumer>
  {headerHeight => (
    /* render something */
  )}
</HeaderHeightContext.Consumer>
```

Ref: [react-navigation](https://github.com/react-navigation/react-navigation)

## Dimensions

[Dimensions](https://reactnative.dev/docs/dimensions/)

```js
import { useWindowDimensions } from "react-native";
```

> Unlike Dimensions, it updates as the window's dimensions update.

```js
import { Dimensions } from "react-native";
const windowWidth = Dimensions.get("window").width;
const windowHeight = Dimensions.get("window").height;

useEffect(() => {
  Dimensions.addEventListener("change", onChange);
  return () => {
    Dimensions.removeEventListener("change", onChange);
  };
});
```

## Device Information

[react-native-device-info](https://github.com/react-native-device-info/react-native-device-info)

```js
let hasNotch = DeviceInfo.hasNotch();
```

## AppState

[AppState](https://reactnative.dev/docs/appstate)

> AppState can tell you if the app is in the foreground or background, and notify you when the state changes.

## React Native Async Storage

[Async Storage](https://github.com/react-native-async-storage/async-storage)

> Internally to AsyncStorage, all keys you provide are prepended with a unique identifier to reference your application to segment storage needs between apps.

[Extreme Optimization of AsyncStorage in React Native](https://medium.com/@Sendbird/extreme-optimization-of-asyncstorage-in-react-native-b2a1e0107b34)

```js
const clearAppData = async function () {
  try {
    const keys = await AsyncStorage.getAllKeys();
    await AsyncStorage.multiRemove(keys);
  } catch (error) {
    console.error("Error clearing app data.");
  }
};
```

```js
import { Platform } from "react-native";
import AsyncStorage from "@react-native-community/async-storage";

const asyncStorageKeys = await AsyncStorage.getAllKeys();
if (asyncStorageKeys.length > 0) {
  if (Platform.OS === "android") {
    await AsyncStorage.clear();
  }
  if (Platform.OS === "ios") {
    await AsyncStorage.multiRemove(asyncStorageKeys);
  }
}
```

[https://github.com/MiRinZhang/react-native-expire-storage](https://github.com/MiRinZhang/react-native-expire-storage)

```bash
npm i -S react-native-expire-storage
```

## Open Settings

```js
import { TouchableOpacity, Linking } from "react-native";
const Component = (props) => {
  return (
    <TouchableOpacity
      activeOpacity={0.8}
      onPress={() => Linking.openURL("app-settings:")}
    >
      <SettingsIcon />
    </TouchableOpacity>
  );
};
```

```js
import { openSettings } from "react-native-permissions";
const Component = (props) => {
  return (
    <TouchableOpacity activeOpacity={0.8} onPress={() => openSettings()}>
      <SettingsIcon />
    </TouchableOpacity>
  );
};
```

Ref: [React Native: Managing App Permissions for iOS](https://medium.com/@rossbulat/react-native-managing-app-permissions-for-ios-4204e2286598)

> Linking to the app-settings: URL will jump directly into the app’s settings within the Settings app.

## React Native Permissions

```bash
 npm install --save react-native-permissions
```

[react-native-permissions](https://github.com/zoontek/react-native-permissions#readme)

[opensettings()](https://www.npmjs.com/package/react-native-permissions#opensettings)
[Permissions statuses](https://www.npmjs.com/package/react-native-permissions#permissions-statuses)

> On the old version, we have two methods: `canOpenSettings` and `openSettings`. Now we have only one that will be rejected if it's not possible. To perform an action when the app is getting focus back, you can use (AppState)[https://facebook.github.io/react-native/docs/appstate]
