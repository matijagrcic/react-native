# Tel Link

```js
if (Platform.OS === "ios") {
  phoneNumber = `telprompt:${phone}`;
} else {
  phoneNumber = `tel:${phone}`;
}
Linking.canOpenURL(phoneNumber);
```

# Lottie

```jsx
function NavigationLottieView(props) {
  const isPlayedRef = React.useRef(false);
  const lottieViewRef = React.useRef(null);

  useFocusEffect(
    React.useCallback(() => {
      if (isPlayedRef.current) {
        lottieViewRef.current?.resume();
      } else {
        isPlayedRef.current = true;
        lottieViewRef.current?.play();
      }

      return () => lottieViewRef.current?.pause();
    }, [])
  );

  return <LottieView ref={lottieViewRef} {...props} />;
}
```

# On App Launch

```jsx
import { useAppState } from "@react-native-community/hooks";

const onAppLaunchRef = React.useRef < boolean > false;
const appState = useAppState();

// code can be running when app state is not active, but `useEffect` with an empty dependency array will be running on first app launch.
useEffect(() => {
  if (onLaunchRef.current) {
    return;
  }

  if (appState !== "active") {
    return;
  }

  //do something here
  onLaunchRef.current = true;
}, []);
```
