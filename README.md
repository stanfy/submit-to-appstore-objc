# submit-to-appstore-objc

Checklist for iOS developer before submitting app to AppStore. 


## iTunesConnect & developer.apple.com
  * You have installed publisher's provision profile (containing private key p12).
  * You have installed distribution certificate containing your app BundleID.
  * You have prepared app in iTunesConnect with your app's BundleID. Description and l10ns are provided for all relevant languages.
  
## APNS
  * App's BundleID is used in APNS certificate.
  * You have created distribution APNS certificate.
  * Your server is using distribution APNS certificate.

## Versioning
  * You haven't set anywhere in the app `isBeta=YES` or `DEBUG=YES`.
  * You haven't set in any server requests `beta=1`.
  * App icon & name doesn't contain `beta` word.
  * You have updated version and build version, and you never use it in hardcoded way (use CFBundleVersion instead).
  * App connects to the production server URL.
  * [Crashlytics](https://crashlytics.com) is enabled.
  * [Flurry](http://www.flurry.com/) is enabled.
  * You've checked that new release (using f.e. ad-hoc distribution) is installed on old version in correct way. 
    * Data from NSUserDefaults is read in correct way (app doesn't crash trying to read unexisting keys).
    * If app uses server configurated data, it's updating in correct way. If it needs to be updated every N hours - it's really get updated.
    
    
## In-App Purchases
  * You have submitted finance docs (without doing it, app doesn't receive even list of in-apps):
  ![iTunesConnect notification message](pics/apns-finance-error.png)
  * If you've hardcoded in-apps IDs, they should be the same in iTunesConnect app too.
  * In-apps are displaying correctly. Test user can make purchase.
  * In-apps are submitted for review! Otherwise in-apps won't be available even if app version was reviewed.
  
  
## Specific services
### Parse.com
  * ApplicationId and ClientKey are connected to production DB.
  * Production DB uses Distribution APNS Certificate, that is created for current app BundleID.
  * Cloud code is deployed to production DB!
  
### Facebook
  * Make sure, that you are using production app, check client key and perform successful login/sharing to Fb.
  * Disable Sandbox mode for Fb app.
  * If you are using GraphStory, send them to review, describe steps-to-reproduce and add necessary screenshots.