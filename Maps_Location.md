- [Packages](#packages)
  - [React Native Maps](#react-native-maps)
  - [React Native Location](#react-native-location)
  - [React Native Geolocation Service](#react-native-geolocation-service)
  - [React Native Geolocation](#react-native-geolocation)
  - [React Native Open Maps](#react-native-open-maps)
  - [React Native Map Link](#react-native-map-link)
  - [React Native Maps Directions](#react-native-maps-directions)
- [TypeScript and Google Maps](#typescript-and-google-maps)
- [Parse Google Maps Address_Components](#parse-google-maps-address_components)
  - [Apps](#apps)

# Packages

## React Native Maps

[react-native-maps](https://github.com/react-native-maps/react-native-maps)

[Installation](https://github.com/react-native-maps/react-native-maps/blob/master/docs/installation.md)

[Android Maps Utilities](https://mvnrepository.com/artifact/com.google.maps.android/android-maps-utils)

[Google APIs for Android](https://developers.google.com/android/guides/releases)

[MapView Methods](https://github.com/react-native-maps/react-native-maps/blob/master/docs/mapview.md#methods)

[Visual Explanation animateToRegion](https://stackoverflow.com/questions/36685372/how-to-zoom-in-out-in-react-native-map/36688156#36688156)

```xml
<meta-data
        android:name="com.google.android.geo.API_KEY"
        android:value="YOUR_API_KEY"/>
```

[Docs](https://github.com/react-native-maps/react-native-maps/tree/master/docs)

[Examples](https://github.com/react-native-maps/react-native-maps/tree/master/example/examples)

[Blog - Introduction to react-native-maps](https://blog.logrocket.com/introduction-to-react-native-maps/)

## React Native Location

[react-native-location](https://github.com/timfpark/react-native-location)

## React Native Geolocation Service

[react-native-geolocation-service](https://github.com/Agontuk/react-native-geolocation-service)

> Uses the recommended `Google Location Services API`.

```bash
npm install react-native-geolocation-service
```

[Examples](https://github.com/Agontuk/react-native-geolocation-service/tree/master/example)

```js
if (Platform.OS !== "android") {
  Geolocation.requestAuthorization();
} else {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION,
      {
        title: "",
        message: "",
        buttonNeutral: "Ask Me Later",
        buttonNegative: "Cancel",
        buttonPositive: "OK",
      }
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
    } else {
    }
  } catch (error) {}
}
```

info.plist

```txt
NSLocationWhenInUseUsageDescription
NSLocationAlwaysUsageDescription
NSLocationAlwaysAndWhenInUseUsageDescription
```

AndroidManifest.xml

```xml
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

Ref: [Setup](https://github.com/Agontuk/react-native-geolocation-service/blob/master/docs/setup.md)

## React Native Geolocation

[react-native-geolocation](https://github.com/react-native-geolocation/react-native-geolocation)

> Uses the `android.location` API which is not recommended by Google because it is less accurate and slower than the recommended `Google Location Services API`.

## React Native Open Maps

[react-native-open-maps](https://github.com/brh55/react-native-open-maps)

## React Native Map Link

[react-native-map-link](https://github.com/flexible-agency/react-native-map-link)

## React Native Maps Directions

[react-native-maps-directions](https://github.com/bramus/react-native-maps-directions)

[Example](https://github.com/bramus/react-native-maps-directions-example)

# TypeScript and Google Maps

```bash
npm i -D @types/googlemaps
```

Reference: [TypeScript and Google Maps](https://developers.google.com/maps/documentation/javascript/using-typescript)

# Parse Google Maps Address_Components

```js
const address = address_components.reduce((seed, { long_name, types }) => {
  types.forEach((t) => {
    seed[t] = long_name;
  });

  return seed;
}, {});
```

[How to parse google maps Address components. (geocoder response)](https://medium.com/@almestaadmicadiab/how-to-parse-google-maps-address-components-geocoder-response-774d1f3375d)

## Apps

How to spoof your location on Android

- Download a GPS spoofing app
- Enable Developer options
- Select mock location app
- Spoof your location

[Fake GPS GO Location Spoofer Free](https://play.google.com/store/apps/details?id=com.incorporateapps.fakegps.fre)
[Fake GPS location](https://play.google.com/store/apps/details?id=com.lexa.fakegps)
