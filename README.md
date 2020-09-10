[![Generic badge](https://img.shields.io/badge/License-MIT-green.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/Android-YES-green.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/iOS-NO-red.svg)](https://shields.io/)
[![Ask Me Anything !](https://img.shields.io/badge/Tested-No-1abc9c.svg)](https://GitHub.com/Naereen/ama)
[![Ask Me Anything !](https://img.shields.io/badge/Published-No-1abc9c.svg)](https://GitHub.com/Naereen/ama)

# React Native In-App Update

React Native In-App Update is a library that does App updates within your app easily, making sure your users are always up to date.
This library supports at the moment Android only.

## 🎉 Getting started

To get started and make sure to configure it well please learn more about Play Store in-app updates [here](https://developer.android.com/guide/playcore/in-app-updates) first.

`$ yarn add react-native-in-app-update`
or
`$ npm install react-native-in-app-update --save`

### Mostly automatic installation

`$ react-native link react-native-in-app-update`

### Manual installation

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`

-   Add `import com.franznkemaka.RNInAppUpdatePackage;` to the imports at the top of the file

-   Add `new RNInAppUpdatePackage()` to the list returned by the `getPackages()` method

2. Append the following lines to `android/settings.gradle`:
    ```
    include ':react-native-in-app-update'
    project(':react-native-in-app-update').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-in-app-update/android')
    ```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:

    ```
      compile project(':react-native-in-app-update')
    ```

## ℹ️ Usage

```javascript
import RNInAppUpdate from 'react-native-in-app-update';

componentDidMount(){
   // check for updates and show modal if available
   // on iOS this displays a warning as it not supported
   InAppUpdate.checkUpdate();
}
```

Suggest to restart app

```javascript
componentDidMount(){
  InAppUpdate.checkUpdate();
  InAppUpdate.onUpdateDownloaded((completeUpdate)=> {
     // new update was download but not yet installed
     // reload app to apply changes

     Alert.alert(
        'Update Downloaded',
        'An update has just been downloaded. Restart app to apply changes',
        {
          text:'Restart',
          onPress: () => {
            // you can terminate the update hence restarting the app
            InAppUpdate.forceCompleteUpdate();
          }
       })
  });
}
```

## 🏗 API

### Recap

-   `FLEXIBLE` means that the update is for example optional and can be downloaded in the background while the user is using the app.

-   `IMMEDIATE` means that the update must be downloaded and a full screen is displayed while downloading.

-   `staleDays` defines the number of days after which an update is not FLEXIBLE but becomes IMMEDIATE instead, hence forcing the user to update.

### Methods

#### `checkUpdate(config: UpdatesConfigObject) :void`

```typescript
type UpdatesConfigObject = {
    staleDays?: number; // default 5
};
```

#### `onUpdateDownloaded(callback: CallableFunction) :void`

Fires when the update was in `FLEXIBLE` mode and it finished downloading. With your callback you can show an alert to prompt the user to restart or something alike.

#### `forceCompleteUpdate() :void`

Use this function in `onUpdateDownloaded` to terminate the update process by restarting the app.

## 🤝 Authors and acknowledgment

-   [@franznkemaka](https://github.com/franznkemaka)
-   Thanks to [@sandeshnaroju](https://github.com/sandeshnaroju) for his initial work done with [react-native-in-app-update](https://github.com/sandeshnaroju/react-native-in-app-update) and with [this article](https://www.naroju.com/implementing-android-in-app-updates-in-react-native)

## 📌 Roadmap

-   [x] 🤖 Add Android support
-   [ ] 🍏 Add iOS Support
-   [ ] ✨ Add Priority mode, [as described here](https://developer.android.com/guide/playcore/in-app-updates#check-priority)

## ❤️ Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## ⚖️ License

This project is licensed under the [MIT](LICENSE) License
