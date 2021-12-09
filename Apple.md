#Why iOS display a permission alert only for FaceID?

This is a deliberate UX choice on Apple's part. It's having to do with the passive nature of Face ID (simply continuing to look at the device) vs. the intentional action a user takes to place their finger on the Touch ID sensor on the device. Without an interstitial asking for deliberate permission to use the feature, a user may inadvertently (successfully) authenticate with Face ID despite potentially having no intent to do so.

The behavior you detailed in your question is clearly documented in [Logging a User into Your App with Face ID or Touch ID](https://developer.apple.com/documentation/localauthentication/logging_a_user_into_your_app_with_face_id_or_touch_id)

> In any project that uses biometrics, include the NSFaceIDUsageDescription key in your app’s Info.plist file. Without this key, the system won’t allow your app to use Face ID. The value for this key is a string that the system presents to the user the first time your app attempts to use Face ID. The string should clearly explain why your app needs access to this authentication mechanism. The system doesn’t require a comparable usage description for Touch ID.

> Touch ID, once locked-out due to incorrect tries, will be locked until the user enters the passcode. So there is no set time. The only way to unlock will be the passcode from this point onwards and there is no way to force an unlock, for obvious reasons.

> Biometrics becomes "locked" on iOS after multiple failed attempts, and will remain locked until the user enters their passcode.

# Touch ID Simulator

> Features -> Touch ID Enrolled to make the Touch ID active

> Features -> Simulate Finger Touch -> Matching or Non-Matching

[Three New App Status Indicators in iTunes Connect](https://developer.apple.com/news/?id=08022010a)

_Prepare for Upload_ indicates that you have created a new version, but you have not yet clicked the Ready to Submit Binary button, which indicates that you are ready to deliver a binary through Application Loader. This state’s status color is yellow.

_Pending Developer Release_ indicates that the version of your app has been approved by App Review and you have turned on the Version Release Control, but have not yet clicked Send Version Live. This state’s status color is yellow. You should also see a pending action symbol on the version. Your version will remain in this state, and thus will not be live on the App Store until you click Send Version Live.

_Processing for App Store_ indicates that the version is being processed to go live on the App Store. Once the processing is complete, the version state will change to "Ready for Sale." This state is very temporary (1-2 hours). This state’s status color is yellow.
