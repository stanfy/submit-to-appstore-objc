# submit-to-appstore-objc

Checklist for iOS developer before submitting app to AppStore. 


## iTunesConnect & developer.apple.com
  * You have installed publisher's provision profile containing private key p12.
  * You have installed distribution certificate containing your app BundleID.
  * You have prepared app in iTunesConnect with your app BundleID. Description and l10ns are provided for all relevant languages.
  
## APNS
  * Your app has BundleID equal to one in APNS certificates.
  * You have created distribution APNS certificate.
  * Your server is using distribution APNS certificate.

## Versioning
  * You haven't set anywhere in the app `isBeta=YES` or `DEBUG=YES`
  * You haven't set in any server requests `beta=1`
  * App icon & name doesn't contain `beta` word
  * You have updated version and build version, and you never use it in hardcoded way (use CFBundleVersion instead)
  * App connects to the production server URL
  * [Crashlytics](https://crashlytics.com) is enabled
  * [Flurry](http://www.flurry.com/) is enabled
  * You've checked that new release (using f.e. ad-hoc distribution) is installed on old version in correct way. 
    * Data from NSUserDefaults is reading in correct way (app doesn't crash trying to read unexciting keys).
    * If app uses server configurated data, it's rewritting in correct way. If it needs to be updated every N hours - it really get updated.