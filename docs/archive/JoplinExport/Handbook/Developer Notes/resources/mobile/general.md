---
title: general
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Deciding on a framework for mobile development

## Goals
* Rapid development.
    * Trying to get a quick prototype up and running to test out the feasability of the project
* Web initially
    * Create the equivalent of a mobile web site that can be packaged as a native app later. Can be a combination of both web and native.
* IOS first
    * Focused on developing an IOS app. Will port to Android. Maybe to Windows based on the framework.
* Web framework
    * Use JavaScript, CSS, HTML for putting together project.

## Tools
* Apache Cordova - underlying tool for the hybrid platform.
* AngularJS - JavaScript framework that seems to be most portable to NativeScript.
* TypeScript - write JavaScript with enterprise tools.

## Frameworks
* Ionic - Angular and typescript. Has an infrastructure around it. Can generate components with command line.
* Framework7 - Seems to have a variety of templates.
* OnsenUI - just not enough for me to bite.

## Thinking
* Starting with Framework7 template tool. See how far we can get. Goal is to create a web site that will suffice as a prototype for mobile site.
    * Not going to use Framework7. Uses less for css.
* Going to try and use ionic framework.

## Progressive Web Apps
* [Progressive Angular Applications](https://houssein.me/progressive-angular-applications)

# Mobile Notes

## Mobile Prototyping Tools
* [Marvel](https://marvelapp.com/features/) - Prototyping tool. Has a free tier.
* [Axure](https://www.axure.com/#a=features) - Has a free educational version.
* [Aquro](http://www.aquro.com/pricing) - Has free tier.
* [Vectr](https://vectr.com/) - Free. Includes for web.
* [Invision](https://www.invisionapp.com/) - Web and mobile prototype
* [Zeplin](https://zeplin.io/) - Free for single project.

### Web only
* [CSS3 Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) - use for interactivity
* [Hammer](http://hammerjs.github.io/) - JavaScript library for touch.

## Mobile Web UI Kits
* [Framework7](https://framework7.io/)
* [UIKit](https://getuikit.com/docs/installation)
* [OnsenUI](https://onsen.io)
* [Aura](https://github.com/forcedotcom/aura) - Java backen
    * [Aura Documentation](http://documentation.auraframework.org/auradocs)
* [Mobile Angular UI](http://mobileangularui.com/)
* [Ratchet](http://goratchet.com/)

## Native Kits
* [NativeScript](http://docs.nativescript.org/)
* [AppCelerator](http://www.appcelerator.com/)

## Hybrid Kits
* [Ionic 2](http://ionicframework.com/docs/intro/installation/) - Uses Angular
* [PhoneGap](https://phonegap.com/) - uses Cordova
* [Cordova](https://cordova.apache.org/) - Underlying tool for most hybrid kits

## Libraries
* [Hammer](http://hammerjs.github.io/) - JavaScript library for touch.
* [Angular](https://angular.io/) - Library that seems to be the underlying framework for most hybrid apps.
* [Zepto](http://zeptojs.com/) - replacement for jquery.

## Tools
* [Google Developer Tools](https://developers.google.com/products/develop/)
* [LimeJS](https://github.com/digitalfruit/limejs) - [Web Page](http://www.limejs.com/) - Game framework.

## Services
* [Googel Firebase](https://firebase.google.com/)
* [Keen IO](https://keen.io/) - api for event data

## UI Kit Templates
* [UpLabs](https://ios.uplabs.com/) - UI kit market.

## Agencies
* [Famous](https://famous.co/)

## Online App Template Building Tools
* [AppInstitute](https://appinstitute.com/pricing/)
* [AppMachine](http://www.appmachine.com/)
* [AppMakr](https://www.appmakr.com/)
* [AppYourself](https://appyourself.net/en/)
* [Appery](https://appery.io/)
* [Creator](http://ionic.io/products/creator/pricing)
* [Swiftic](https://www.swiftic.com/features/)
* [Kinvey](https://www.kinvey.com/)
* [App Press](https://www.app-press.com/) - Code free app development
* [EachScape](https://eachscape.com/) - Drag and drop interfaces
* [iBuildApp](https://ibuildapp.com/) - Online app creator
* [ViziApps](http://www.viziapps.com/) - Create mobile apps
* [AppGyver](https://www.appgyver.eu/) - App gyver

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

# Ionic Development Notes
Trying to figure out Ionic while building a prototype to demo via the web.
## Notes
* Pushing site to gh-pages.
    * Ref: [Deploying an Angular App to Github Pages](https://alligator.io/angular/deploying-angular-app-github-pages/)
    * Ionic starter template includes the manifest and worker file by default.
    * Use the ionic build scripts to create the web version of your app.
    1. Install *angular-cli-ghpages* globally
        * `npm install --global angular-cli-ghpages`
    1. Build ionic app with base-href to github gh-url for your username
        * `npm run ionic:build --prod --base-href "https://<username>.github.io/<repository>/"`
    1. Push to gh-pages. `ngh --dir www` - have to use *www* because the script looks for the *dist* folder by default.
