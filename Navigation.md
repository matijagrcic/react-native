# TabNavigator

> TabNavigator is not shipped with a Header. The most common case is to make your TabNavigator the root navigator, and make each tab a StackNavigator you would then get the header cause it's part of the StackNavigator by default.

[Hiding tab bar in specific screens](https://reactnavigation.org/docs/hiding-tabbar-in-screens/)

[createMaterialTopTabNavigator](https://reactnavigation.org/docs/material-top-tab-navigator/)

```bash
npm install @react-navigation/material-top-tabs react-native-tab-view
```

# Navigation Options

_Root Navigator_ - used to switch between major navigation flows of the app, consists of

- auth flow - registration, login, etc
- main flow - uses Main Navigator

_Main Navigator_ - displays an auth flow or other user flows

Strongly typed navigators `createStackNavigator<Type>`  
Would prefer if we use MobX State Tree store(s) to handle state rather than navigation params
