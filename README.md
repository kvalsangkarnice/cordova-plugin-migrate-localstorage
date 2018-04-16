# Migrate LocalStorage from UIWebview to Ionic WKWebView

This plugin can be used in conjunction with
[cordova-plugin-ionic-webview](https://github.com/ionic-team/cordova-plugin-ionic-webview)
to persist LocalStorage data when migrating from `UIWebView` to ionic's `WKWebView`. All related
files will be copied over automatically during startup so the user can simply pick up where they
left of.

## How to use

Simply add the plugin to your cordova project via the cli:
```sh
cordova plugin add https://github.com/paulpatarinski/cordova-plugin-migrate-localstorage
```

## Notes

- LocalStorage files are only copied over once and only if no LocalStorage data exists for ionic's `WKWebView`
yet. This means that if you've run your app with `WKWebView` before this plugin will likely not work.
To test if data is migrated over correctly:
    1. Delete the app from your emulator or device
    2. Remove `cordova-plugin-migrate-localstorage`
    
    ```
    cordova plugin rm cordova-plugin-migrate-localstorage
    ```
    3. Remove the `cordova-plugin-ionic-webview`
    
    ```
    cordova plugin rm cordova-plugin-ionic-webview
    ```

    4. Run your app and store some data in LocalStorage
    5. Add both plugins back
   
     ```
    cordova plugin add cordova-plugin-ionic-webview@1.1.16
    ```
    
    ```
    cordova plugin add https://github.com/paulpatarinski/cordova-plugin-migrate-localstorage
    ```
   
    6. Run your app again. Your data should still be there!

- Once the data is copied over, it is not being synced back to `UIWebView` so any changes done in
`WKWebView` will not persist should you ever move back to `UIWebView`. If you have a problem with this,
let us know in the issues section!

## Background

One of the drawbacks of migrating Cordova apps to `WKWebView` is that LocalStorage data does
not persist between the two. Unfortunately,
[cordova-plugin-ionic-webview](https://github.com/ionic-team/cordova-plugin-ionic-webview)
does not offer a solution for this out of the box.

## Disclaimer
This plugin has only been tested with cordova-plugin-ionic-webview v1.1.16, so use at your own risk.

## Credits

This plugin is a fork of a [fork](https://github.com/kas84/cordova-plugin-migrate-localstorage) of a [copy](https://github.com/MaKleSoft/cordova-plugin-migrate-localstorage) of the [Telerik WKWebView source](https://github.com/Telerik-Verified-Plugins/WKWebView/blob/master/src/ios/MyMainViewController.m), so all props go to someone else. #open-source