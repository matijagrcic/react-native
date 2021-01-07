# Hot Reload changes on iPhone thru your Windows

Build with a mac and then continue with any other os.
With an iPhone:

- install the app on the iPhone through your mac(run-ios)

- launch the bundler on your windows pc (react-native start)

- pick up your ipv4 address on windows (ipconfig)

- enter the ipv4 address on the rn app's dev menu

Now you can hot reload any changes on your iPhone through your windows pc.
It works as long as you don't change the package.json, because than you have to run-ios again on your mac.

# Custom Header

```jsx
export const YourCustomHeader = (props: YourCustomHeaderProps) => {
  return (
    <SafeAreaView>
      <View
        style={{
          height: 60,
          backgroundColor: "white",
          flexDirection: "row",
          alignItems: "center",
          paddingLeft: 20,
          paddingRight: 20,
        }}
      >
        <View
          style={{
            flex: 1,
            flexDirection: "row",
            justifyContent: "flex-start",
          }}
        >
          {props.leftComponent}
        </View>
        <View
          style={{
            flex: 1,
            justifyContent: "center",
            alignItems: "center",
            flexDirection: "row",
          }}
        >
          <Text
            style={{
              color: "black",
              fontSize: 16,
            }}
          >
            {props.title}
          </Text>
        </View>
        <View
          style={{ flex: 1, flexDirection: "row", justifyContent: "flex-end" }}
        >
          {props.rightComponent}
        </View>
      </View>
    </SafeAreaView>
  );
};
```
