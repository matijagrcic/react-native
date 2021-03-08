`AsyncStorage.clear()` errors on iOS but not Android.

`AsyncStorage.getAllKeys().then(AsyncStorage.multiRemove)` errors on Android but not iOS.

```jsx
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

[Storing and Retrieving Objects using AsyncStorage in React Native](https://medium.com/@richardzhanguw/storing-and-retrieving-objects-using-asyncstorage-in-react-native-6bb1745fdcdd)
