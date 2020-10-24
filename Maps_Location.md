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

# Packages

## React Native Maps

[react-native-maps](https://github.com/react-native-maps/react-native-maps)

[Installation](https://github.com/react-native-maps/react-native-maps/blob/master/docs/installation.md)

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

[Examples](https://github.com/Agontuk/react-native-geolocation-service/tree/master/example)

```js
if (Platform.OS !== 'android') {
  Geolocation.requestAuthorization();
} else {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION,
      {
        title: '',
        message: '',
        buttonNeutral: 'Ask Me Later',
        buttonNegative: 'Cancel',
        buttonPositive: 'OK',
      }
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
    } else {
    }
  } catch (error) {}
}
```

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
