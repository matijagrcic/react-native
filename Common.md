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
