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

> Prevents reinventing the wheel.

Internal libraries for whole team to use:

- UI elements, layouts
- Authentication and Networking
- Brand UI elements, colors and themes
- Data persistance and logging

# Navigation Options

_Root Navigator_ - used to switch between major navigation flows of the app, consists of

- auth flow - registration, login, etc
- main flow - uses Main Navigator

_Main Navigator_ - displays an auth flow or other user flows

Strongly typed navigators `createStackNavigator<Type>`

> Having a well-defined app navigation strategy with good separation of app state is key for any decent-sized app.

> Many teams only build this map once they code themselves in a corner, discovering they have built inconsistent navigation solutions that lead to bugs when the user gets in unexpected states.

# State Managment

> Challenges of native apps are not similar to that on the web

> App life cycle events and transitions are not a cause for concern in the web and backend world

> Most bugs and unexpected crashes are usually caused by an unexpected or untested combination of events and the application's state

> The larger and more complex the app, the more likely bugs are caused by a combination events that are out of the ordinary.

Leverage isolate component(s) and application state as much as possible and tend to start using reactive state management. Keep state as immutable as possible, storing models as immutable objects that emit state changes. (practice at Uber, Airbnb etc.)

> Deeplinks are connected to state management and the navigation architecture (plan ahead for them)

> Push notifications are "glorified" deeplinks (they also link into the app and are connected to state and navigation architecture)

# Accessibility

> If the app is not accessible there is an inherent legal risk and your users will find the app difficult if not impossible to interact with

> App quality increases as you make it more accessible

- Implementing accessibility from the start is a low effort on iOS and a sensible one for Android (both platforms make it relatively painless to add accessibility features)
- Retrofitting accessibility is time-consuming

# Testing

> Manual testing is a viable path in small app. If you're not doing a decent level of automated testing on a large app, you're digging yourself in a hole.

Mocked live data for testing:

- speed
- edge cases - setup mock data for edge case scenarios
- reliability
- frequency - immediate feedback, avoids running tests only pre-merge which results in longer feedback loop
