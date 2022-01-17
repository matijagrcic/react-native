# Fastlane

- Testing
- Screenshots
- Build
- Signing
- Prepare Push Certificate
- Upload
- Processing
- Submit for review

> Only thing needed in CI/CD is `fastlane nameOfTheLane` given fastfile is in a version control.

## Goals

- Automatic Deployment
- Version Control (build scripts)
- Developer Independent

> Creating screenshots (new screenshots for each version) - great to see if app looks ok on all the screens

## Code Signing (provision profiles)

- Code Signing Identity (certificate and private key) - Apple Recommends that each dev has it's own Code Signing Identity
- Provisioning Profile (connection between code signing identity and and APP Identifier, stored in App Dev Portal)
- Building & Signing
- Signed IPA

Stored in GIT allows easy onboarding

- Distribution Certificate
- Development Certificate
- App Store Provisioning Profile
- Development Provisioning Profile

[https://codesigning.guide/](https://codesigning.guide/)

```bash
#asks for git repo url and stores certificates and profiles there
fastlane match init

#clones git repo and installs certificate and provisioning profile
fastlane match appstore
```

```ruby
desc "Deploy a new version to the App Store"
lane :appstore do
  match(type: "appstore") #fetch all signing certificates and provisioning profiles
  snapshot #create the screenshots for your app
  gym #build your app for the app store
  deliver(force: true) #upload screenshots, metadata, and the archive to iTunes Connect
  frameit #create marketing images with device frames from your screenshots
end
```

[Make Fastlane Snapshot Work with React Native](https://fanchenbao.medium.com/make-fastlane-snapshot-work-with-react-native-babd5c5b0cee)

[Make Fastlane Screengrab Work with React Native](https://fanchenbao.medium.com/make-fastlane-screengrab-work-with-react-native-da14f7138920)

### Automatic Deployment

- Version bump
- Commit & Push
- Provisioning Profile
- Build
- Export
- Upload
- Add Release Notes
- Distribute

> Fastfile - passes information from one build step to the next one

```bash
#runs a beta lane
fastlane beta
```

```bash
fastlane init #gonna create `appfile` and `fastfile`

fastlane lanes #see defined lanes
```

# Aliases

- `deliver` aka `upload_to_app_store`
- `match` aka `sync_code_signing`
- `supply` aka `upload_to_play_store`
- `pilot` aka `upload_to_testflight`
- `gym` aka `build_ios_app`
- `produce` aka `create_app_online`

# Android process

- Build APK
- Generate a private key

```ruby
  gradle(task: "assembleRelease)
```

- Code Sign APK with the private key
- Upload signed APK to Google Play

```bash
cd android
cd secure

keytool -gen key -v keystore myapp-key.keystore -alias myapp-key-alias -keyalg RSA -keysize 2048 -validity 10000

#follow other prompts
```

```ruby
  supply(
  track: "alpha", #alpha, beta, production, internal
  apk: "#{lane_context[SharedValues:: GRADLE_APK_OUTPUTH_PATH]}"
  )
```

- Distribute private key to another team members
- Fill out app info in Google Play, Upload Screenshots
- Initial release

```java
// android > app > build.gradle
// in .env.default you can define the env variables which fastlane will load
signingConfigs {
    release {
        storeFile file(System.getenv("RELEASE_STORE_FILE")) //path to the myapp-key.keystore
        storePassword System.getenv("RELEASE_STORE_PASSWORD") //password
        keyAlias System.getenv("RELEASE_KEY_ALIAS") //myapp-key-alias
        keyPassword System.getenv("RELEASE_KEY_PASSWORD")  //password
    }
}
```

```java
//android > app > build.gradle
buildTypes {
    release {
        signingConfig signingConfigs.release
    }
}
```

```bash
./gradlew assembleRelease #will generate APK under `android > app > build > outputs > apk > release`
```

# Upload to Google Play Console

> First release is manual every other is automated thru Fastlane

- Get API key
- Go to Settings > Developer Account > API access > Service Accounts > Create Service Account > follow the steps
- Under Role give it Owner (or whatever is needed)
- Create key and choose JSON
- Grant access
- Go to - Create Application
- Fill out metadata
- Go to - App release - click on Review then Start rollout to Alpha

```bash
fastlane init

# Grab applicationId from android > app > build.gradle
# Enter path to json secret key file
# Accept downloading metadata to your computer
```

```ruby
desc "Alpha release"
lane :alpha do

    # app > src > AndroidManifest.xml
    # fastlane add_plugin increment_version_code
    # will increment `versionCode` under `defaultConfig` in build.gradle
    increment_version_code(
        gradle_file_path: "./app/build.gradle"
    )
    gradle (task: "assembleRelease")
    supply(
        track: "alpha", #alpha, beta, production
        apk: "#{lane_context[SharedValues:: GRADLE_APK_OUTPUTH_PATH]}"
    )
end

desc "Beta release"
lane :beta do

    # app > src > AndroidManifest.xml
    # fastlane add_plugin increment_version_code
    # will increment versionCode in build.gradle
    increment_version_code(
        gradle_file_path: "./app/build.gradle"
    )
    gradle (task: "assembleRelease")
    supply(
        track: "beta", #alpha, beta, production
        apk: "#{lane_context[SharedValues:: GRADLE_APK_OUTPUTH_PATH]}"
    )
end

desc "Production release"
lane :production do

    #app > src > AndroidManifest.xml
    #fastlane add_plugin increment_version_code
    #will increment versionCode in build.gradle
    increment_version_code(
        gradle_file_path: "./app/build.gradle"
    )
    gradle (task: "assembleRelease")
    supply(
        track: "production", #alpha, beta, production
        apk: "#{lane_context[SharedValues:: GRADLE_APK_OUTPUTH_PATH]}"
    )
end
```

# iOS process

- Increment build number - increment_build_number
- Install dependencies with Cocoapods - cocoapods
- Build IPA - gym or build_app
- Generate or grab latest Production Provisioning Profile - match
- Create sealed IPA - gym or build_app
- Upload sealed IPA to the app store - deliver or upload_to_app_store
- Capture and upload screenshots to app store - snap, deliver or upload_to_app_store
- Fill out metadata in Apple Connect - deliver or upload_to_app_store
- Submit app for review - deliver or upload_to_app_store

```bash
fastlane produce # generates app shell on Apple Connect and Identifier on Apple Developer Portal
fastlane init # follow the prompts
```

```json
{
  "alcoholTobaccoOrDrugUseOrReferences": "NONE",
  "contests": "NONE",
  "gamblingSimulated": "NONE",
  "horrorOrFearThemes": "NONE",
  "matureOrSuggestiveThemes": "NONE",
  "medicalOrTreatmentInformation": "NONE",
  "profanityOrCrudeHumor": "NONE",
  "sexualContentGraphicAndNudity": "NONE",
  "sexualContentOrNudity": "NONE",
  "violenceCartoonOrFantasy": "NONE",
  "violenceRealisticProlongedGraphicOrSadistic": "FREQUENT_OR_INTENSE",
  "violenceRealistic": "INFREQUENT_OR_MILD",
  "gambling": false,
  "seventeenPlus": false,
  "unrestrictedWebAccess": true
}
```

[Ref](https://github.com/fastlane/fastlane/blob/master/deliver/assets/example_rating_config.json)

# Fastlane env files

> .env is loaded automatically by fastlane

> In .env define the following, used by fastlane tools

```bash
FASTLANE_USER=Apple Developer Account
FASTLANE_TEAM_NAME=First and Last Name
FASTLANE_ITC_TEAM_NAME=First and Last Name

PRODUCE_APP_IDENTIFIER=com.myapp.demo
PRODUCE_APP_NAME=My App Demo
PRODUCE_VERSION=0.1.0
PRODUCE_SKU=MY_APP_010
PRODUCE_PLATFORMS=ios

MATCH_USERNAME=Apple Developer Account
MATCH_GIT_URL=URLTOTHEREPO
MATCH_APP_IDENTIFIER=com.myapp.demo
MATCH_TYPE=appstore
MATCH_PLATFORM=ios

#fastlane action update_code_signing_settings
FL_PROJECT_SIGNING_PROJECT_PATH=
FL_PROJECT_SIGNING_TARGETS=
FL_PROJECT_SIGNING_BUILD_CONFIGURATIONS=
FL_PROJECT_USE_AUTOMATIC_SIGNING=false
FL_CODE_SIGN_IDENTITY=Apple Distribution

GYM_SCHEME=
GYM_EXPORT_METHOD=app-store
GYM_OUTPUT_DIRECTORY=build/ios

DELIVER_APP_IDENTIFIER=com.myapp.demo
DELIVER_TEAM_NAME=First and Last Name
DELIVER_DEV_PORTAL_TEAM_NAME=First and Last Name
DELIVER_RUN_PRECHECK_BEFORE_SUBMIT=false
DELIVER_SKIP_SCREENSHOTS=true
DELIVER_SKIP_METADATA=true

.env.secret

#needed if account has 2FA enabled
FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=

# DAV, Aspera, Signiant
DELIVER_ITMSTRANSPORTER_ADDITIONAL_UPLOAD_PARAMETERS=-t Aspera

DELIVER_PLATFORM=ios

```

```ruby
desc "Create app on Developer Portal and App Store Connect"
lane :create_app do
    create_app_online #produce
end


fastlane_require "dotenv"

before_all do
        #load the specific env
        Dotenv.load ".env.secret"
end

platform :ios do
    before_all do
        #load the specific env
        Dotenv.load ".env.ios"
        Dotenv.load ".env.secret"
    end

    desc "Create keys, certificates and provisioning profiles, Distribution cert stored in keychain, profiles stored and encrypted in Git repo"
    lane :sign_app do
        match #sync_code_signing

        # after match runs it puts the value to lane_context singleton
        # we don't need to sign into XCode and `Automatically manage signing` doesn't work on CI so we prefer manual signing but thru fastlane
        mapping = Actions.lane_context[SharedValues::MATCH_PROVISIONING_PROFILE_MAPPING]

        #Modifies Xcode build settings for target/configuration
        update_code_signing_settings(
            profile_name: mapping[ENV["MATCH_APP_IDENTIFIER"]]
        )
    end

    desc "Build"
    lane :build_app do
        sign_app

        # uses xcodebuild, installs SPM dependencies, compiles the app, signs and exports binary
        gym #build_ios_app
    end

    desc "Release"
    lane :release_app do
        ensure_git_status_clean
        ensure_git_branch

        add_git_tag
        push_git_tag

        build_app
        # uploads binary to App Store Connect
        deliver #upload_to_app_store

        #does git checkout -- for modified files
        reset_git_repo

        set_bitbucket_release
    end
end
```

> Spaceship - communicates with Apple (iTunes connect, Apple Developer portal, API Xcode uses)

[https://spaceship.airforce/](https://spaceship.airforce/)

[https://github.com/fastlane/fastlane/tree/master/spaceship](https://github.com/fastlane/fastlane/tree/master/spaceship)

> Boarding - Instantly create a simple signup page for TestFlight beta testers.

[https://github.com/fastlane/boarding#readme](https://github.com/fastlane/boarding#readme)

[https://appetize.io/](https://appetize.io/)

> Run native mobile apps in your browser

# Screenshots

[https://docs.fastlane.tools/getting-started/android/screenshots/](https://docs.fastlane.tools/getting-started/android/screenshots/)
[https://docs.fastlane.tools/getting-started/ios/screenshots/](https://docs.fastlane.tools/getting-started/ios/screenshots/)

# Commands

```
fastlane deliver download_metadata
fastlane deliver download_screenshots
```

## Talks

## MCE^3 - Felix Krause - Continuous Delivery for Mobile Apps Using Fastlane

[![MCE^3 - Felix Krause - Continuous Delivery for Mobile Apps Using Fastlane](https://img.youtube.com/vi/wOtANfkh2bI/0.jpg)](https://www.youtube.com/watch?v=wOtANfkh2bI)

[Slides](https://speakerdeck.com/krausefx/mceconf-warsaw)

## Automating Your App's Release Process Using Fastlane (Firebase Dev Summit 2017)

[![Automating Your App's Release Process Using Fastlane (Firebase Dev Summit 2017)](https://img.youtube.com/vi/scfOk5SgrKU/0.jpg)](https://www.youtube.com/watch?v=scfOk5SgrKU)

## iOS Continuous Delivery with Fastlane – Felix Krause

[![iOS Continuous Delivery with Fastlane – Felix Krause](https://img.youtube.com/vi/qGKzJ8HmZLw/0.jpg)](https://www.youtube.com/watch?v=qGKzJ8HmZLw)

## iOS Pipeline with Fastlane by Felix Krause (Twitter)

[![iOS Pipeline with Fastlane by Felix Krause (Twitter)](https://img.youtube.com/vi/AaJf2Uf36m0/0.jpg)](https://www.youtube.com/watch?v=AaJf2Uf36m0)

## Implementing Fastlane from nothing to App Store, Josh Holtz (English)

[![Implementing fastlane from nothing to App Store, Josh Holtz (English)](https://img.youtube.com/vi/6Jz-Ywxki0U/0.jpg)](https://www.youtube.com/watch?v=6Jz-Ywxki0U)

## Philippe Trepanier - Automate your React Native world with fastlane

[![Philippe Trepanier - Automate your React Native world with fastlane](https://img.youtube.com/vi/1K5OLv3moFg/0.jpg)](https://www.youtube.com/watch?v=1K5OLv3moFg)

## Repos

[Firebase App Distribution](https://github.com/fastlane/fastlane-plugin-firebase_app_distribution)

# Blogs

[Shipping React Native apps with Fastlane](https://carloscuesta.me/blog/shipping-react-native-apps-with-fastlane)

# Tutorials

[React Native Fastlane Release Automation](https://www.youtube.com/playlist?list=PLrw-z7lfJTHetXKnHBYIThqoMZWfaMdz1)

# Documentation

[Getting started with fastlane for React Native](https://docs.fastlane.tools/getting-started/cross-platform/react-native/)
