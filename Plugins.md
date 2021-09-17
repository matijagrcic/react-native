# React Native Reanimated Bottom Sheet

[Reanimated Bottom Sheet](https://github.com/osdnk/react-native-reanimated-bottom-sheet)

```bash
npm install reanimated-bottom-sheet
npm install react-native-reanimated react-native-gesture-handler
```

```jsx
<BottomSheet
  snapPoints={[0, hp("60%"), ACTUAL_SCREEN_HEIGHT]}
  initialSnap={1}
  onOpenEnd={() => {
    this.setState({ allowScrolling: true });
  }}
  enabledInnerScrolling={true}
  onCloseStart={() => this.setState({ allowScrolling: false })}
  onCloseEnd={() => this.props.onBackdropPress()}
  enabledGestureInteraction={true}
  overdragResistanceFactor={0}
  enabledHeaderGestureInteraction={true}
  enabledContentGestureInteraction={!this.state.allowScrolling}
  renderContent={this.renderContent}
  renderHeader={this.renderHeader}
/>
```

[VirtualizedList](https://reactnative.dev/docs/virtualizedlist)

```jsx
<VirtualizedList
  showVerticalScrollIndicator={false}
  ref={(ref) => (this.scrollView = ref)}
  onScroll={(event) => {
    if (event.nativeEvent.contentOffset.y < 10) {
      this.setState({ allowScrolling: false });
    }
  }}
  data={this.props.options}
  getItemCount={(data) => this.props.options.length}
  getItem={(data, index) => {
    return data[index];
  }}
  keyExtractor={(item, index) => {
    return item.id;
  }}
  onEndReached={() => console.log("End Reached")}
  renderItem={this.renderItem}
/>
```

> If you want the inner content to be scrollable when using `VirtualizedList` in the `BottomSheet`, make sure `enabledContentGestureInteraction` is set to `false`.

[VirtualizedList](https://reactnative.dev/docs/virtualizedlist)

> The difference between the `FlatList` implementation and the `VirtualizedList` is the need to define `getItem` and `getItemCount`.

[Normalizing State Shape](https://redux.js.org/recipes/structuring-reducers/normalizing-state-shape#designing-a-normalized-state)

```js
const data = {
  byId: {
    0: {},
    1: {},
    2: {},
  },
  allIds: [0, 1, 2],
};
```

## Inner content not scrollable

> Import `ScrollView` or `FlatList` from `react-native-gesture-handler` that works on android without any other workarounds.

# React Native Scroll Bottom Sheet

[Scroll Bottom Sheet](https://github.com/rgommezz/react-native-scroll-bottom-sheet)

```bash
npm install react-native-scroll-bottom-sheet
npm install react-native-reanimated react-native-gesture-handler
```

# React Native Bottom Sheet

[react-native-bottom-sheet](https://github.com/gorhom/react-native-bottom-sheet)

> Clone of React Native Scroll Bottom Sheet but fully rewritten.

```bash
npm install @gorhom/bottom-sheet
npm install react-native-reanimated react-native-gesture-handler
```

```bash
npm install @gorhom/bottom-sheet@2.0.0-alpha.0 #react-native-reanimated v2
npm install react-native-reanimated@alpha react-native-gesture-handler
```

# React Native Raw Bottom Sheet

[react-native-raw-bottom-sheet](https://github.com/nysamnang/react-native-raw-bottom-sheet)

```bash
npm i react-native-raw-bottom-sheet --save
```

# React Native Modalize

[react-native-modalize](https://github.com/jeremybarbet/react-native-modalize)

```bash
npm i react-native-modalize react-native-gesture-handler
```

[Documentation](https://jeremybarbet.github.io/react-native-modalize/#/)

# React Native Safe Area View

[react-native-safe-area-view](https://github.com/react-navigation/react-native-safe-area-view)

```js
import { useSafeArea } from ‘react-native-community/react-native-safe-area-view’;

const insets = useSafeArea();
return <View style={{ paddingTop: insets.top }} />; //can also [forceInset](https://github.com/react-navigation/react-native-safe-area-view#forceinset)

```

Ref: [SafeAreaView react-navigation to fix iPhone X design issue](https://medium.com/@maheshnandam/use-safeareaview-from-react-navigation-to-fix-iphone-x-design-issue-ba531a9181d)
Ref: [SafeAreaView](https://reactnative.dev/docs/safeareaview)

# React Native Safe Area Context

> Works on Android and Web!

[react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context)

```bash
npm install react-native-safe-area-context
```

import { SafeAreaProvider } from 'react-native-safe-area-context';

```js
function App() {
  return <SafeAreaProvider>...</SafeAreaProvider>;
}
```

# React Native Floating Bubble

> A simple Facebook Chat Head like bubble for react native.

```bash
npm install react-native-floating-bubble --save
```

```js
import {
  showFloatingBubble,
  hideFloatingBubble,
  requestPermission,
} from "react-native-floating-bubble";

// Show Floating Bubble
showFloatingBubble().then(() => console.log("Floating Bubble Added"));
```

# React Native Config

[react-native-config](https://github.com/luggit/react-native-config)

[Setup Android](https://github.com/luggit/react-native-config#extra-step-for-android)

[More info](https://www.bigbinary.com/blog/handling-environment-specific-configurations-in-react-native)

[Handling environment specific configurations in React Native](https://www.bigbinary.com/blog/handling-environment-specific-configurations-in-react-native)

react-native run-ios --scheme "Dev"
react-native run-ios --scheme "Prod"
Xcode goes to Product -> Schemes -> Manage Schemes... -> (Plus icon to create new scheme).
You can manage the configurations choosing the Edit option.

To list all available schemes for the project in your current directory
xcodebuild -list
xcodebuild -list -workspace ./MyApp.xcworkspace
xcodebuild -list -project ./MyApp.xcodeproj

# React Native FS

[react-native-fs](https://github.com/itinance/react-native-fs)

# React Native Clean Project

[react-native-clean-project](https://github.com/pmadruga/react-native-clean-project)

Deleted yarn.lock
Deleted node_modules & pods
yarn install
pod install --repo-update

# Async-Storage Flipper

[rn-async-storage-flipper](https://github.com/Fausto95/rn-async-storage-flipper)

## React Native Permissions

```bash
 npm install --save react-native-permissions
```

[react-native-permissions](https://github.com/zoontek/react-native-permissions#readme)

[opensettings()](https://www.npmjs.com/package/react-native-permissions#opensettings)
[Permissions statuses](https://www.npmjs.com/package/react-native-permissions#permissions-statuses)

> On the old version, we have two methods: `canOpenSettings` and `openSettings`. Now we have only one that will be rejected if it's not possible. To perform an action when the app is getting focus back, you can use (AppState)[https://facebook.github.io/react-native/docs/appstate]

# React Native Collapsible

[react-native-collapsible](https://github.com/oblador/react-native-collapsible)

# React Native Collapsible View

[react-native-collapsible-view](https://github.com/Eliav2/react-native-collapsible-view)

# React Native Collapsible List

[react-native-collapsible-list](https://github.com/hamidhadi/react-native-collapsible-list)

# React Native Version Check

[react-native-version-check](https://github.com/kimxogus/react-native-version-check)

```jsx
useEffect(() => {
  checkUpdateNeeded();
}, []);

const checkUpdateNeeded = async () => {
  let updateNeeded = await VersionCheck.needUpdate();
  if (updateNeeded.isNeeded) {
    //Alert the user and direct to the app url
  }
};

const latestVersion = await VersionCheck.getLatestVersion();
const currentVersion = VersionCheck.getCurrentVersion();
```

# React Native Hold Menu

[react-native-hold-menu](https://github.com/enesozturk/react-native-hold-menu)

# React Native Calendars

[react-native-calendars](https://github.com/wix/react-native-calendars)

# React Native Bundle Visualizer

[react-native-bundle-visualizer](https://github.com/IjzerenHein/react-native-bundle-visualizer)

# React Native Cookies

[react-native-cookies/cookies](https://github.com/react-native-cookies/cookies)

# React Native Picker

[react-native-picker/picker](https://github.com/react-native-picker/picker)

# Shadow Generator

[https://ethercreative.github.io/react-native-shadow-generator/](https://ethercreative.github.io/react-native-shadow-generator/)

# React Native PDF

[react-native-pdf](https://github.com/wonday/react-native-pdf)
