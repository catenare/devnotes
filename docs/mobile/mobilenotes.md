# Mobile Device Development Notes

## Android
* Google Tools
    * [Android Studio](https://developer.android.com/studio/index.html)

### Solutions
* **Problem:** Launching Android SDK Manager without going through Atom Studio
  * *~/Library/Android/sdk/tools/android*
  * **For AVD** *~/Library/Android/sdk/tools/android avd*
      * [StackOverflow](http://stackoverflow.com/questions/16271242/launch-android-sdk-manager-tools-directory-doesnt-exist-mac)
      * Lauch AVD - [StackOverflow](http://stackoverflow.com/questions/8119282/dont-see-android-sdk-and-avd-manager-when-execute-android-tool-command)

## IOS
### IOS Development Notes

* Cocoapods
    * Issue: *Unable to add a source with url https://github.com/CocoaPods/Specs.git named master. You can try adding it manually in ~/.cocoapods/repos or via pod repo add*
    * [StackOverflow](http://stackoverflow.com/questions/33649114/since-i-installed-xcode-7-1-1-and-updatet-on-osx-10-11-1-i-get-an-git-error)
```
    cd ~/.cocoapods/repos
    git clone git://github.com/CocoaPods/Specs.git master
    pod install --no-repo-update --verbose
```
* Actual issue: I'm in South Africa and it was taking forever to do the initial repo specs checkout. Doing git clone git:/github.com/CocoaPods/Specs.git master into ~/.cocoapods/repos resolved the problem. Going forward, only has to update the repos, not completely download it.

## Resources
* [Android Developer - Google](https://developer.android.com/index.html))
* [Some Teaching Notes - ](https://www3.ntu.edu.sg/home/ehchua/programming/android/Android_HowTo.html#zz-2.)

### Tools
* [Fastlane](https://fastlane.tools/) - release tool for mobile app.
* [App Inventor](http://appinventor.mit.edu/explore/)
* [Cocos2d-x](http://www.cocos2d-x.org/) - IOS Game dev tools.