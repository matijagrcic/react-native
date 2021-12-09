The recommended best-practice is to now use separate values for _CFBundleShortVersionString_ and _CFBundleVersion_

3-component for _CFBundleShortVersionString_ (ex: 4.2.3)
A build number for _CFBundleVersion_

> The _CFBundleShortVersionString_ is the version shown on the App Store. The _CFBundleVersion_ will need to change for every build you upload.

_CFBundleShortVersionString_ gives you the version of your app.
It's typically incremented each time you publish your app to the App Store.
This is the version that is visible on the "Version" section for the App Store page of your application.

_CFBundleVersion_ gives you the build number which is used for development and testing, namely "technical" purposes. The end user is rarely interested in the build number but during the development you may need to know what's being developed and fixed on each build. This is typically incremented on each iteration of internal release. And you can use continuous integration tools like Jenkins to auto-increment the build number on each build.

[CFBundleVersion](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleversion)
[CFBundleShortVersionString](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleshortversionstring)

[Version Numbers and Build Numbers](https://developer.apple.com/library/archive/technotes/tn2420/_index.html)


[increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/)