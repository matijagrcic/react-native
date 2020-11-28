- Density Independent Pixels: React Native’s pixel unit of measurement
- Flexbox: Make your layouts flexible by default
- Dimensions: Calculate sizes/position based on device dimensions
- Percentages: Dimensions Relative to its container
- PixelRatio: Handle sizing depending on pixel depth

> A component can only expand to fill available space if its parent has dimensions greater than 0. If a parent does not have either a fixed width and height or flex, the parent will have dimensions of 0 and the flex children will not be visible.

Ref: [Flex Dimensions](https://reactnative.dev/docs/height-and-width#flex-dimensions)

# Material Design Tabs

> 48dp (inline text) or 72dp (non-inline text and icon)

Ref: [Tabs](https://material.io/develop/android/components/tabs)

```js
navigationOptions: () => ({
  tabBarLabel: ({ focused }) => (
    <MyTabBarLabel title={i18n.t("common.request")} focused={focused} />
  ),
  tabBarIcon: ({ focused }) => (
    <MyTabBarIcon icon="requests" focused={focused} />
  ),
});
```

Ref: [Customizing the appearance](https://reactnavigation.org/docs/tab-based-navigation/#customizing-the-appearance)
