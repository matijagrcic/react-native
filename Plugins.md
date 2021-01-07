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
