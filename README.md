# submit-to-appstore-objc

Checklist for iOS developer before submitting app to AppStore. 


## iTunesConnect & developer.apple.com
  * Install publisher's provision profile (containing private key p12).
  * Install distribution certificate containing your app BundleID.
  * Prepare app in iTunesConnect with your app's BundleID. 
  * Provide description and l10ns for all relevant languages.
  * Provide screenshosts/videos in iTunesConnect.
  
  
## APNS
  * APNS certificate inclued your app's BundleID.
  * You have created distribution APNS certificate.
  * Your server is using distribution APNS certificate.
  * Check that pushes are working on different iOS versions (pay attention on **iOS8** where API was changed).
  

## Versioning
  * Do not hardcode anywhere in sources things like `isBeta=YES` or `DEBUG=YES`.
  * App icon & name doesn't contain `beta` word.
  
  * Update app version and build version. And never harcode it inside app (use CFBundleVersion instead).
  
  * **IMPORTANT** Check that new release is installed on old version in correct way. 
    * Install app from AppStore. Create ad-hoc build and install it over.
    * Check that data from NSUserDefaults is read in correct way (app doesn't crash trying to read unexisting keys).
    * Check that user won't lose any his info after update.  
  
  
## Server
  * Connect application to production server environment. 
  * Do not send `beta=1` (or similar) in any server requests.
  * If app uses server configurated data, it's updating in correct way. If configuration needs to be updated every N hours - it's really updates.
    
    
## Tools
  * Enable [Crashlytics](https://crashlytics.com).
  * Enable analytics like [Flurry](http://www.flurry.com/).
  * Disable `NSLog` calls. At least like this
  
  ``` objective-c
  #define NSLog(...) /* */
  ```
    
    
## In-App Purchases
  * Enable IAPs for your app id in developer.app.com
  ![app id on developer.apple.com](pics/developer.apple.com-ids.png =600x)
  
  * Enable IAPs in Xcode Build Settings
  ![app id on developer.apple.com](pics/xcode-apns.png =600x)
  
  * Submit finance docs (without doing it, app doesn't receive even list of in-apps) in iTunesConnect:
  ![iTunesConnect notification message](pics/apns-finance-error.png =600x)
  
  * Make sure, that if you've hardcoded IAPs IDs, they are the same in iTunes  Connect app too.  
  ![iTunesConnect IAPs](pics/itunesconnect-IAPs.png =600x)
  
  * In-apps are displaying correctly. Test user can make purchases.
  * In-apps are submitted for review! Otherwise in-apps won't be available even if app version was reviewed.
  
  
## Specific services
### Parse.com
  * Check AppDelegate and make sure that `applicationId` and `clientKey` are used from production account.
  
  **AppDelegate**
  
  ``` objective-c
  // --------------------- Parse credentials:
    [Parse setApplicationId:@"FDF...WGr" clientKey:@"1BzI...F"];
  ```
  
  Parse.com application keys
  ![parse.com keys](pics/parse-keys.png =600x)
  Keys should be the same in Settings and AppDelegate.
  
  
  * Deploy Cloud code to production account!
  * Parse application is marked as 'PROD' in Settings
  ![parse.com settings](pics/parse-production-mode.png =600x)
  
  * If you're using APNS, set production certificate in Settings 
  ![parse.com apns](pics/parse-apns.png =600x)
  
  
### Facebook
  * Make sure, that you are using production app, check client key and perform successful login/sharing to Fb.
  * Disable Sandbox mode for Fb app.
  * If you are using GraphStory, send them to review, describe steps-to-reproduce and add necessary screenshots.