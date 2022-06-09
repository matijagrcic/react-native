[React Native Firebase](https://rnfirebase.io/)

[Disable Analytics data collection - iOS](https://firebase.google.com/docs/analytics/configure-data-collection?platform=ios)

```xml
<key>FIREBASE_ANALYTICS_COLLECTION_ENABLED</key>
<false/>
```

Use [set_info_plist_value](https://docs.fastlane.tools/actions/set_info_plist_value/) with Fastlane

[Disable Analytics data collection - Android](https://firebase.google.com/docs/analytics/configure-data-collection?platform=android)

```xml
<meta-data android:name="firebase_analytics_collection_enabled" android:value="false" />
```

## Track Screenviews

[Track Screenviews](https://firebase.google.com/docs/analytics/screenviews)

```xml
<key>FirebaseAutomaticScreenReportingEnabled</key>
<false/>
```

```xml
<meta-data android:name="google_analytics_automatic_screen_reporting_enabled" android:value="false" />
```

[A New Approach to Firebase Screenview Tracking](https://adswerve.com/blog/a-new-approach-to-firebase-screenview-tracking/)

# DebugView

- set up environment variable `-FIRDebugEnabled`
- run app thru Xcode

or

```bash
xcrun simctl launch "iPhone 13 Mini" com.your.package -FIRDebugEnabled
```

[Debugging Events](https://firebase.google.com/docs/analytics/debugview#ios+)

[View events in the Xcode debug console](https://firebase.google.com/docs/analytics/events?platform=ios#view_events_in_the_xcode_debug_console)

- In Xcode, select `Product > Scheme > Edit scheme...`
- Select `Run` from the left menu.
- Select the `Arguments` tab.
- In the `Arguments Passed On Launch `section, add `-FIRAnalyticsDebugEnabled`.

> The next time you run your app, your events will display in the Xcode debug console, helping you immediately verify that events are being sent.

> Firebase events are batched together and uploaded once every hour in order to prevent excessive battery drain on the devices. On iOS when you background the app before the 1h upload target the events will be dispatched at this time in the background.

> Once the events are uploaded there is delay at about 3h before the data will show up in the Firebase Analytics dashboard. Also the default day range excludes "today" so you only see events from yesterday. You can switch the date picker to include Today if you like to see the latest events.
