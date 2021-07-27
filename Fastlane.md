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

### Creating screenshots (new screenshots for each version) - great to see if app looks ok on all the screens

### Code Signing (provision profiles)

Code Signing Identity (certificate and private key) - Apple Recommends that each dev has it's own Code Signing Identity
Provisioning Profile (connection between code signing identity and and APP Identifier, stored in App Dev Portal)
Building & Signing
Signed IPA

Stored in GIT allows easy onboarding

- Distribution Certificate
- Development Certificate
- App Store Provisioning Profile
- Development Provisioning Profile

[https://codesigning.guide/](https://codesigning.guide/)

```bash
#asks for git repo url and stores certificates and profiles there
match init

#clones git repo and installs certificate and provisioning profile
match appstore
```

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

> Spaceship - communicates with Apple (iTunes connect, Apple Developer portal, API Xcode uses)

> Boarding - Instantly create a simple signup page for TestFlight beta testers.

[https://github.com/fastlane/boarding#readme](https://github.com/fastlane/boarding#readme)

[https://appetize.io/](https://appetize.io/)

> Run native mobile apps in your browser

## Talks

## MCE^3 - Felix Krause - Continuous Delivery for Mobile Apps Using Fastlane

[![MCE^3 - Felix Krause - Continuous Delivery for Mobile Apps Using Fastlane](https://img.youtube.com/vi/wOtANfkh2bI/0.jpg)](https://www.youtube.com/watch?v=wOtANfkh2bI)

[Slides](https://speakerdeck.com/krausefx/mceconf-warsaw)

## Automating Your App's Release Process Using Fastlane (Firebase Dev Summit 2017)

[![Automating Your App's Release Process Using Fastlane (Firebase Dev Summit 2017)](https://img.youtube.com/vi/scfOk5SgrKU/0.jpg)](https://www.youtube.com/watch?v=scfOk5SgrKU)

## Implementing Fastlane from nothing to App Store, Josh Holtz (English)

[![Implementing fastlane from nothing to App Store, Josh Holtz (English)](https://img.youtube.com/vi/6Jz-Ywxki0U/0.jpg)](https://www.youtube.com/watch?v=6Jz-Ywxki0U)
