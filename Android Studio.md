# Gradle Sync Failed

- Run `open -a /Applications/Android\ Studio.app`
- sync Gradle

or

`sudo ln -s "$(which node)" /usr/local/bin/node`
In `android/gradle/wrapper/gradle-wrapper.properties` update to `distributionUrl=https\://services.gradle.org/distributions/gradle-6.9-all.zip`
then execute `cd android && ./gradlew clean`.
