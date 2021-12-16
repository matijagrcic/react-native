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

# Density Independent Pixels

> All dimensions in React Native are unitless, and represent density-independent pixels. Setting dimensions this way is common for components that should always render at exactly the same size, regardless of screen dimensions.

Units in React Native are in dp. If you want to convert them to pixels, use `PixelRatio.getPixelSizeForLayoutSize()`

> Density independent pixel ( or a device independent pixel ) is an absolute unit of measurement like inches, centimeters or millimeters. _The value for 1 dp equals 1/160 of inch or 0.15875 mm_

> 1dp equals to 1 pixel on a medium-density screen (160dpi or 160 dots per inch or 160ppi)

`px = dp * (dpi / 160)`

> Since a screen can have such a difference in how many pixels are drawn on it, it doesn’t make much sense to have a coordinate space that uses pixels, it would be very difficult to place items on a screen with that large of a variation of units.

> Coordinate space separate from the resolution of the device. This makes it much more simpler to place items.

[Ref](http://www.embusinessproducts.com/handling-different-screen-sizes-react-native/)

_Density qualifier_

- ldpi Resources for low-density (ldpi) screens (~120dpi).
- mdpi Resources for medium-density (mdpi) screens (~160dpi). (This is the baseline density.)
- hdpi Resources for high-density (hdpi) screens (~240dpi).
- xhdpi Resources for extra-high-density (xhdpi) screens (~320dpi).
- xxhdpi Resources for extra-extra-high-density (xxhdpi) screens (~480dpi).
- xxxhdpi Resources for extra-extra-extra-high-density (xxxhdpi) uses (~640dpi).

[Ref](https://developer.android.com/training/multiscreen/screendensities#TaskUseDP)
[Pixel Ratio](https://reactnative.dev/docs/pixelratio#methods)

> PixelRatio is handy for sizing images and fonts.
