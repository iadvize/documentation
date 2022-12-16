# iAdvize Messenger SDK : Integration guide

This document aims to help you integrate the iAdvize Messenger SDK into your mobile applications.

## ⚙️ Prerequisites

### 💬 Setting up your iAdvize environment

Before integrating the SDK, you need to check that your iAdvize environment is ready to use (i.e. you have an account ready to receive and answer to conversations from the SDK).
You will also need some information related to the project for the SDK setup. Please ask your iAdvize administrator to follow the instructions available on the [SDK Knowledge Base](https://help.iadvize.com/hc/en-gb/articles/360019839480) and to provide you with the **Project Identifier** as well as a **Targeting Rule Identifier**.

> *⚠️ Your iAdvize administrator should already have configured the project on the [iAdvize Administration Desk](https://ha.iadvize.com/admin/login/) and created an operator account for you. If it is not yet the case please contact your iAdvize Technical Project Manager.*

### 💻 Connecting to your iAdvize Operator Desk

Using your operator account please log into the [iAdvize Desk](https://ha.iadvize.com/admin/login/).

> *⚠️ If you have the Administrator status in addition to your operator account, you will be directed to the Admin Desk when logging in. Just click on the `Chat` button in the upper right corner to open the Operator Desk.*

The iAdvize operator desk is the place where the conversations that are assigned to your account will pop up. Please ensure that your status is “Available" by enabling the corresponding chat or video toggle buttons in the upper right corner:

![The chat button is green, your operator can receive incoming conversations.](./assets/images/mobile-sdk/01-operator-desk.png)

If the toggle button is yellow, it means you have reached your maximum simultaneous chat slots, please end your current conversations to free a chat slot and allow the conversations to be assigned to you. If the toggle is red you are not available to chat.

### ⚛️ Finding the SDK for your platform

The iAdvize Messenger SDK is developped and released for the native mobile platforms (Android/iOS). Plugins for bridging with the native SDK are also provided for some hybrid platforms (ReactNative/Flutter).

> *⚠️ Please note that there may be delays between Native SDK releases and the corresponding hybrid plugins update deliveries.*

| Platform | Demo | API Reference | Documentation |
| --- | --- | --- | --- |
| Android | [GitHub](https://github.com/iadvize/iadvize-android-sdk) | [Dokka](https://iadvize.github.io/iadvize-android-sdk/) | [Integration](https://developers.iadvize.com/documentation/mobile-sdk-android) |
| iOS | [GitHub](https://github.com/iadvize/iadvize-ios-sdk) | [Jazzy](https://iadvize.github.io/iadvize-ios-sdk/) | [Integration](https://developers.iadvize.com/documentation/mobile-sdk-ios) |
| ReactNative | [GitHub](https://github.com/iadvize/iadvize-react-native-sdk) | | [Integration](https://developers.iadvize.com/documentation/mobile-sdk-reactnative) |
| Flutter | [GitHub](https://github.com/iadvize/iadvize-flutter-sdk) | | [Integration](https://developers.iadvize.com/documentation/mobile-sdk-flutter) |

To proceed with the SDK integration, please follow the link to the documentation corresponding to your mobile platform.