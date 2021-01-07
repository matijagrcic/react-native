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
