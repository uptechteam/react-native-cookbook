# Intro
There is a pretty good article about building RN deployment pipeline with FastLane, CircleCI, CodePush and AppCenter:

[Build the React Native Deployment Pipeline of Your Dreams](https://blog.theodo.com/2019/04/react-native-deployment-pipeline)


Read it fully before actually doing anything, to better understand the whole picture.

You may think _"Ok, link to the article, so why do we have a page in the cookbook for it?"_. Reasonable, so here I provide you with some tips, that I learned through blood, sweat and tears.

# Tips

* ⚠️ Pay attention to Android keystore files!

  >Pay attention to Android Keystore files (especially for production, after your uploaded APK to Google Play Console), because if you will delete it or rewrite it with a command by mistake - you will lose the ability to update your app in Google Play Console. That leads to creating a new app, that will make a customer not very happy. (That's why in Uptech Google Play Console account we have "SandboxMobileApp(deprecated)")
  It's better to backup Keystore files after first creation to some safe place before proceeding with the next commands from the article, so then you will have your back safe.


* Fix for `yo rn-toolbox:fastlane-env` command.

  If you use modern RN, you probably don't need to run `react-native link` command and you don't have react-native installed globally.

  That's why at the end of `yo rn-toolbox:fastlane-env` command you will get this error:

  ```
  Linking AppCenter CodePush for you...
  PLEASE LEAVE THE KEY FIELDS BLANK.
  Configuration went well but there was an error while installing AppCenter CodePush. Please install it manually with `react-native link react-native-code-push`. Then rerun the generator.
  Error: spawnSync react-native ENOENT
  ```

  This is because "fastlane-env" script has `react-native link` commands, and we can simply remove them.

  To do so, navigate to `/Users/{userName}/.config/yarn/global/node_modules/generator-rn-toolbox/generators/fastlane-env/index.js` and replace `_reactNativeLinkDependencies()` with this function:

  ``` js
  _reactNativeLinkDependencies() {
      if (this.answers.useAppcenterSDK) {
        this.log('Installing CocoaPods (please provide sudo password)...');
        this._runInstallCommandsWithErrorMessages(
          cocoaPodsInstallCommands,
          'CocoaPods',
          'sudo gem install cocoapods && cd ios && pod init && pod repo update.'
        );
      }
  }
  ```

* Fix for `bundle exec fastlane ios setup --env=staging`.
  
  Just remove '=' sign. Should be `bundle exec fastlane ios setup --env staging`

* 2FA in your Apple ID while running in CI.

  If you have 2FA in your account, command will ask you to write the code from SMS. It's not a problem if you run script locally, but in CI you can't write it.

  You can fix it by adding apple_id (id of the app from AppStore) to the pilot():

  ```
  lane :deploy_to_testflight do |options|
    pilot(
      username: ENV['IOS_APPSTORECONNECT_USER_ID'],
      app_identifier: ENV['IOS_APP_ID'],
      apple_id: '1540297681',                  <---- here
      ipa: ENV['IOS_IPA_PATH'],
      distribute_external: false,
      skip_waiting_for_build_processing: true
    )
  end
  ```

* AppCenter suggestion
  
  You can omit the creation of the production variant of the app in AppCenter if you will use TestFlight and internal testing.


# Example app (Sandbox Mobile App)

While learning this, I created the sandbox app for test purposes. You can use it as a reference to check configuration files, etc.

[Github](https://github.com/uptechteam/Sandbox-Mobile-App)

[Github repo for Match](https://github.com/uptechteam/Sandbox-Mobile-App-ios-certs)

You can also find it in `Google Play Console`, `Firebase`, `AppCenter`.

Because of some problem with Notification setups (related to Apple Developer Keys) - I created the `iOS` version under my personal App Store Connect account. So, if you will need access to it - just send me PM (Dmitry Rudiuk).

>* Match Repo pass: `Dimon4350489`
>* Unpack secrets pass: `uptechsandbox` for both development and production.
