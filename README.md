# Rhodes Firebase Cloud Messaging Test

## Firebase Cloud Messaging Set Up
Open https://console.firebase.google.com and create Firebase Project.

### Adding iOS App to your Firebase project

You need to get the APNs Auth key (preferred) or the SSL certificate for Apple Push Notifications service (APNs). You can find more details in the article “Configuring APNs with FCM”. Also don’t forget to obtain Apple provision profile with Push Notification capability.

Press iOS icon under the caption “Get started by adding Firebase to your app” or go to Project settings and add the “Add app” button  in General Settings. You can reach Project Settings by pressing the icon “Gear” on the right of the project title at the left top of screen. 

Adding iOS to your Firebase project steps:
  1. Register the app. <br/> Copy the build.yml >> iPhone >> bundleIdentifier into  the field iOS Bundle ID.
  2. Download config file. <br/> Download GoogleService-info.plist file and put it into the root of your Rhodes project.
  3. Add Firebase SDK. <br/> Just skip the step
  4. Add initialization code. <br/> Just skip the step
  5. Read the start guide for iOS. <br/> Go to the console.

Go to the Project Settings >>Cloud Messaging Settings and upload APNs Auth key, specify Key ID and you Apple development team ID.

### Adding Android App to your Firebase project
Press Android icon under the caption “Get started by adding Firebase to your app” or go to Project settings and add the “Add app” button  in General Settings. You can reach Project Settings by pressing the icon “Gear” on the right of the project title at the left top of screen. 
Adding Android to your Firebase project steps:

  1. Register the app. <br/> Fill the “Android package name” field.
  2. Download config file. <br/>  Download google-service.json file and put it into the root of your Rhodes project.
  3. Add Firebase SDK <br/> Just skip the step
  4. Read the start guide for Android <br/> Go to the console.


Now all are ready for building the apps and install it on the devices.

## Building Rhodes App

### iOS build
Run the following commands:

`rake build:iphone:setup_xcode_project`

`rake device:iphone:production`

Open xCode and install the .ipa file to your iOS device. Run the app and it shows the device identifier. The device identifier is required for sending the push messages. It is a long string, so it will be better to copy it from the app’s logs. You can get access to the app’s logs if start the app via xCode.

### Android build
Run the following command:

`rake run:android:device`

Run the app and it shows the device identifier. The device identifier is required for sending the push messages. It is a long string, so it will be better to copy it from the app logs. You can get access to the app’s logs by the command:

`adb logcat -s APP`


## Send your first push notification

Go to console.firebase.google.com, open your project >> Grow >>Cloud Messaging.
Press “Send your first message” button. Fill the Notification Title and Notification Text fields, then press “Send test message” button. Add your device identifiers for iOS app and Android App and press “Test” button. Your apps must show received push notification.
