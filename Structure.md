# App structure

The inside of the app directory looks similar to the following:

```
app
│── components (where components will live)
├── models (where models will live)
├── navigation (where react-navigation navigators will live)
├── screens (where screen components will live)
├── services (REST APIs, Push Notifications, etc.)
├── theme (general app theme, including spacing, colors, and typography)
├── utils (helpers and utilities)
├── app.tsx (entry point to the app)
assets (where static resources will live)
```

# Navigation Options

_Root Navigator_ - used to switch between major navigation flows of the app, consists of

- auth flow - registration, login, etc
- main flow - uses Main Navigator

_Main Navigator_ - displays an auth flow or other user flows

Strongly typed navigators `createStackNavigator<Type>`

Would prefer if we use MobX State Tree store(s) to handle state rather than navigation params
