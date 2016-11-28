# IOS Development Notes

* Cocoapods
  * Issue: *Unable to add a source with url https://github.com/CocoaPods/Specs.git named master. You can try adding it manually in ~/.cocoapods/repos or via pod repo add*
    * [StackOverflow](http://stackoverflow.com/questions/33649114/since-i-installed-xcode-7-1-1-and-updatet-on-osx-10-11-1-i-get-an-git-error)

    ```
    cd ~/.cocoapods/repos
    git clone git://github.com/CocoaPods/Specs.git master
    pod install --no-repo-update --verbose
    ```
    * Actual issue: I'm in South Africa and it was taking forever to do the initial repo specs checkout. Doing git clone git:/github.com/CocoaPods/Specs.git master into ~/.cocoapods/repos resolved the problem. Going forward, only has to update the repos, not completely download it.
