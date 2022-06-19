# Accessibility a11y

WCAG 2.0 Mobile App Guidelines (ensuring all screens are accessible to users)

The WCAG 2.0 has four principles: “Perceivable,” “Operable,” “Understandable” and “Robust.”

- Perceivable means that the presentation of the information and the interface
  components must be in a way that is perceivable to the user.
- Operable means that the users must be able to operate the navigation and user interface.
- Understandable means that the user must be able to understand and how to operate the
  user interface and the information presented to them.
- Robust means that the content must be able to be interpreted reliably by advancing
  technologies and user agents. The content must continue to be accessible.

Each of the four principles in the standard includes guidelines for that
principle, totaling in 12 guidelines. Under each guideline are a number of success criteria.

Perceivable - both content and interface elements must be clearly visible and easy to perceive

- 1.1 Text Alternatives
- 1.2 Time-based Media
- 1.3 Adaptable
- 1.4 Distinguishable

Operable - interface elements are easy to access

- 2.1 Keyboard Accessible
- 2.2 Enough Time
- 2.3 Seizures
- 2.4 Navigable

Understandable - all the messages and operations that can be performed must be understandable with keeping consistent and supporting
multiple orientations layout

- 3.1 Readable
- 3.2 Predictable
- 3.3 Input Assistance

Robust - maximizing compatibility with current and future assistive technologies or tools, but also facilitating the data entry process

**WCAG 2.1** was published the 5th of June 2018 and includes all success criteria from WCAG
2.0 along with 17 new success criteria. These new success criteria now include success criteria
for accessibility in mobile devices, people with low vision and people with cognitive and
learning disabilities (Lawton Henry, 2018c).

Three levels of conformance:

- A (minimum accessibility),
- AA (addresses the major, most common accessibility issues) and
- AAA (the highest standard).

|                                                                                | WCAG 2.0 | WCAG 2.1 | TOTAL WCAG 2.0 and 2.1 |
| ------------------------------------------------------------------------------ | -------- | -------- | ---------------------- |
| A The most basic web accessibility features                                    | 25       | 5        | 30                     |
| AA Deals with the biggest and most common barriers for users with disabilities | 13       | 7        | 20                     |
| AAA The highest (and most complex) level of web accessibility                  | 23       | 5        | 28                     |
| Total                                                                          | 61       | 17       | 78                     |

[How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG21/quickref/?currentsidebar=%23col_customize)

> A customizable quick reference to Web Content Accessibility Guidelines (WCAG) 2 requirements (success criteria) and techniques

[What You Need to Know About WCAG 2.1](https://www.viget.com/articles/what-you-need-to-know-about-wcag-2-1/)

[WCAG 2.2 Quick Reference](https://3pha.com/wcag2/)

[a11ysupport](https://a11ysupport.io/)

> Only about 30% of the WCAG 2.0 success criteria and precisely 0% of the WCAG 2.1 success criteria can be tested using an automated tool.

> Testing tools catch only 30-40% of possible errors.

> Manual testing gives a better perception of the application in the context of a disabled person.

> Divide the application into several parts and assign each developer a section to test then rotate the sections each time so that each developer will check something different every time. The developer will return to the first section and will be familiar with the entire application, which should also reduce the time needed for testing.

[Mobile Accessibility: How WCAG 2.0 and Other W3C/WAI Guidelines Apply to Mobile](https://w3c.github.io/Mobile-A11y-TF-Note/)

[Mobile Accessibility QA Testing Checklist](https://pauljadam.com/demos/mobilechecklist.html#utm_source=microassist&utm_medium=mobilapps&utm_campaign=Pt2)

[What's new in WCAG 2.1, the web Accessibility Standard](https://www.davidmacd.com/blog/wcag-2.1-quick-guide.html)

# VPAT

The Accessibility Conformance Report (ACR) based on the ITI VPAT® is the leading global reporting format for assisting buyers and sellers in identifying information and communications technology (ICT) products and services with accessibility features. Version 2 of the VPAT was expanded to include the leading ICT accessibility standards: Section 508 (U.S.), EN 301 549 (EU), and W3C/WAI WCAG.

- VPAT 2.4 WCAG: WCAG 2.1 or ISO/IEC 40500 – W3C/WAI’s recently updated Web Content Accessibility Guidelines
- VPAT 2.4 508: Revised Section 508 standards – the U.S. Federal accessibility standard
- VPAT 2.4 EU: EN 301 549 – the European Union’s “Accessibility requirements suitable for public procurement of ICT products and services in Europe”
- VPAT 2.4 INT: Incorporate all three of the above standards

[https://www.itic.org/advocacy/resources/?policy=vpat](https://www.itic.org/advocacy/resources/?policy=vpat)

# DHS Section 508 Compliance Test Processes

> Section 508 of the Rehabilitation Act of 1973, as amended (29 U.S.C. 794d), requires all federal departments and agencies to ensure that their electronic information & technology (EIT) is accessible to people with disabilities.

[https://www.dhs.gov/publication/dhs-section-508-compliance-test-processes](https://www.dhs.gov/publication/dhs-section-508-compliance-test-processes)

# Talkback

[https://github.com/google/talkback](https://github.com/google/talkback)

[Talkback Roles](https://github.com/google/talkback/blob/771de7cdbf55b6adb4ca4c64c27a52584f2337cc/compositor/src/main/java/com/google/android/accessibility/compositor/Compositor.java#L733)

On Android, open `Settings > Accessibility > TalkBack` and turn TalkBack on.

# VoiceOver

With an iPhone, go to `Settings > General > Accessibility > VoiceOver`, or simply ask Siri to "Turn
on VoiceOver."

[Accessibility for UIKit](https://developer.apple.com/documentation/uikit/accessibility_for_uikit)

> Make your UIKit apps accessible to everyone who uses iOS and tvOS.

[UIAccessibilityTraits](https://developer.apple.com/documentation/uikit/uiaccessibilitytraits)

> Set these traits to tell an assistive app how an accessibility element behaves or how to treat it.

Accessibility in iOS is define by the `UIAccessibility` protocol which is implemented for all standard UIKit elements (UIView subclasses).

The most important/used properties (but not all) are :

- isAccessibilityElement: if set to yes, the view is the accessibility responsible for itself and all subviews (subview won’t be visible in accessibility)
- accessibilityLabel: a localized string that defines the element (ex « details »)
- accessibilityTraits: explain how your element reacts (like button, text, image, …)
- accessibilityHint: a short description of the result action this element (« will show details »)

> With no accessibility at all elements on the screen are all independent with no logic.

# VoiceOver and TalkBack

**Labeling**

It’s essential that the mobile app is properly coded, with elements correctly labelled, so that they
can be identified correctly by screen readers like iOS’s VoiceOver and Android’s TalkBack. The
code should clearly label the location and purpose of where a user is on a screen and within an
application. Without it, a user who is blind won’t be able to know what they are clicking!

**Gestures**

Gestures—tapping, swiping, pinching, etc.—are vital for users who are blind. When apps do not
respond to native or modified accessibility gestures, it makes it difficult or even impossible for
some people to use.

Both TalkBack and VoiceOver use a variety of touchscreen gestures to help users navigate between content or skip to other content on the page.

> iOS screen reader (VoiceOver) is available only on a physical device

> Android emulator doesn’t have the screen reader (TalkBack) app installed by default

> VoiceOver and Accessibility Inspector tool available via Xcode app

# Web

[Mobile Accessibility Guidelines](https://www.bbc.co.uk/accessibility/forproducts/guides/mobile)

[Accessibility in government](https://accessibility.blog.gov.uk/2016/09/02/dos-and-donts-on-designing-for-accessibility/)

[Accessibility on iOS](https://developer.apple.com/accessibility/ios/)

## Axe

[https://github.com/dequelabs/axe-core#axe-core](https://github.com/dequelabs/axe-core#axe-core)

> Axe is an accessibility testing engine for websites and other HTML-based user interfaces. It's fast, secure, lightweight, and was built to seamlessly integrate with any existing test environment so you can automate accessibility testing alongside your regular functional testing.

[Axe Chrome Extension](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd?hl=en-US)

### Projects that use axe-core

[https://github.com/dequelabs/axe-core/blob/develop/doc/projects.md#projects-that-use-axe-core](https://github.com/dequelabs/axe-core/blob/develop/doc/projects.md#projects-that-use-axe-core)

[axe-core/react](https://www.npmjs.com/package/@axe-core/react)

> Test your React application with the axe-core accessibility testing library. Results will show in the Chrome DevTools console.

[axe-core/playwright](https://www.npmjs.com/package/@axe-core/playwright)
[axe-core/puppeteer](https://www.npmjs.com/package/@axe-core/puppeteer)

[storybook-addon-a11y](https://github.com/storybooks/storybook/tree/master/addons/a11y)

[Automate accessibility tests with Storybook](https://storybook.js.org/blog/automate-accessibility-tests-with-storybook/)

# Tools

[WCAG Accessibility Checklist](https://apps.apple.com/us/app/wcag-accessibility-checklist/id1130086539)

[Accessibility Insights for Web & Android](https://github.com/microsoft/accessibility-insights-web#-accessibility-insights-for-web--android)

> Accessibility Insights for Android is a cross-platform desktop tool used for testing accessibility of Android applications.

[![Introduction to Accessibility Insights for Android](https://img.youtube.com/vi/KuLVuv2yjHc/default.jpg)](https://www.youtube.com/watch?v=KuLVuv2yjHc)

[Accessibility Scanner](https://play.google.com/store/apps/details?id=com.google.android.apps.accessibility.auditor&hl=en_US&gl=US)

[![Accessibility scanner - Accessibility on Android](https://img.youtube.com/vi/i1gMzQv0hWU/default.jpg)](https://www.youtube.com/watch?v=i1gMzQv0hWU)

[Accessibility Inspector in Xcode](https://developer.apple.com/library/archive/documentation/Accessibility/Conceptual/AccessibilityMacOSX/OSXAXTestingApps.html)

[Accessibility Inspector](https://developer.apple.com/videos/play/wwdc2019/257/)

[![Auditing your App with the Accessibility Inspector](https://img.youtube.com/vi/sqGSYGHJMVM/default.jpg)](https://www.youtube.com/watch?v=sqGSYGHJMVM)

[![Accessibility Inspector Tutorial for iOS Native Mobile Apps](https://img.youtube.com/vi/EkG5_kWkqwE/default.jpg)](https://www.youtube.com/watch?v=EkG5_kWkqwE)

[![Voice Over Labels | Accessibility | Swift 4, Xcode 10](https://img.youtube.com/vi/Vyqi_UQRwhI/default.jpg)](https://www.youtube.com/watch?v=Vyqi_UQRwhI)

[Support Full Keyboard Access in your iOS app](https://developer.apple.com/videos/play/wwdc2021/10120/)

# React Native

Properties such as

- accessible,
- accessibilityLabel,
- accessibilityRole or
- accessibilityHint.

[UIAccessibility](https://developer.apple.com/documentation/objectivec/nsobject/uiaccessibility)

> A set of methods that provides accessibility information about views and controls in an app’s user interface.

[eslint-plugin-react-native-a11y](https://github.com/FormidableLabs/eslint-plugin-react-native-a11y)

> This library will validate and ensure correct usage of a11y props when they are in use, but it doesn't force you to implement the props every single time you use a `<Touchable />` or `<Pressable />` component.

> In addition to ensuring the app meets its functional requirements by building tests, it's important that we also ensure our code has no structural problems by running the code through lint. The lint tool helps find poorly structured code that can impact the reliability and efficiency of the app and make the code harder to maintain.

[Accessibility](https://reactnative.dev/docs/next/accessibility)

# Detox

Detox operates within the confines of the native world. Detox doesn't have access to the JS, nor operate at that level. Once an action or an expectation in Detox is run, it travels to the native world, where we observe the native view hierarchy.

[Ref](https://github.com/wix/Detox/issues/2313#issuecomment-689647183)

## React Native - releases focused on accessibility

[Improved React Native Accessibility](https://github.com/facebook/react-native/projects/15)

[React Native Accessibility - GAAD 2022 Update](https://reactnative.dev/blog/2022/05/19/GAAD-2022-update)

[The GAAD Pledge - One Year Later](https://reactnative.dev/blog/2021/05/20/GAAD-One-Year-Later)

[The GAAD Pledge - March Accessibility Issues Update](https://reactnative.dev/blog/2021/04/08/GAAD-March-Accessibility-Issue-Update)

[The GAAD Pledge - Improving React Native Accessibility](https://reactnative.dev/blog/2021/03/08/GAAD-React-Native-Accessibility)

[React Native 0.60](https://reactnative.dev/blog/2019/06/12/react-native-open-source-update#meaningful-community-contributions)

> Accessibility: React Native 0.60 will ship with many improvements to accessibility APIs both on Android and iOS. All of the new features are directly using APIs provided by the underlying platform so they’ll integrate with native assistance technologies both on Android and iOS.

[Accessibility API Updates](https://reactnative.dev/blog/2018/08/13/react-native-accessibility-updates)

## Videos

[VoiceOver efficiency with custom rotors](https://developer.apple.com/videos/play/wwdc2020/10116/)

[SwiftUI Accessibility: Beyond the basics](https://developer.apple.com/videos/play/wwdc2021/10119)

[Writing Great Accessibility Labels](https://developer.apple.com/videos/play/wwdc2019/254/)

[Tailor the VoiceOver experience in your data-rich apps](https://developer.apple.com/videos/play/wwdc2021/10121/)

[Accessibility & Inclusion](https://developer.apple.com/videos/accessibility-inclusion)

[Deque Systems](https://www.youtube.com/user/DequeSystemsInc/videos)

# Blogs

[A smartphone accessibility primer; or, how I learned to stop worrying and master mobile accessibilit](http://simplyaccessible.com/article/smartphone-a11y-primer-1/)

[React Native Accessibility: What, Why, and How?](https://www.callstack.com/blog/react-native-accessibility)

[React Native Android Accessibility Tips](https://www.callstack.com/blog/react-native-android-accessibility-tips)

[Accessibility in React Native](https://www.netguru.com/blog/accessibility-in-react-native)

[Accessibility in React Native Apps](https://levelup.gitconnected.com/accessibility-in-react-native-apps-f06d5469a453)

[Mobile Screen Reader Testing](https://scottvinkle.me/blogs/work/mobile-screen-reader-testing)

[Creating Accessible React Native Apps](https://scottvinkle.me/blogs/work/creating-accessible-react-native-apps)

[VoiceOver vs. Talkback: My Time on the Other Side](https://www.applevis.com/blog/voiceover-vs-talkback-my-time-other-side)

[Intro to the Accessibility Inspector Tool for iOS Native Apps](https://www.deque.com/blog/intro-accessibility-inspector-tool-ios-native-apps/)

[iOS Accessibility: Getting Started](https://www.raywenderlich.com/6827616-ios-accessibility-getting-started#toc-anchor-001)

[Accessibility in iOS with VoiceOver](https://medium.com/geekculture/accessibility-in-ios-ce09f6df992b)
