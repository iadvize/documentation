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

| Platform | Demo project | API Reference | Documentation |
| --- | --- | --- | --- |
| Android | [GitHub](https://github.com/iadvize/iadvize-android-sdk) | [Dokka](https://iadvize.github.io/iadvize-android-sdk/) | [Integration](#android) |
| iOS | [GitHub](https://github.com/iadvize/iadvize-ios-sdk) | [Jazzy](https://iadvize.github.io/iadvize-ios-sdk/) | [Integration](#ios) |
| ReactNative | [GitHub](https://github.com/iadvize/iadvize-react-native-sdk) | | [Integration](#reactnative) |
| Flutter | [GitHub](https://github.com/iadvize/iadvize-flutter-sdk) | | [Integration](#flutter) |

To proceed with the SDK integration, please follow the link to the documentation corresponding to your mobile platform.

## Android

This document aims to help you integrate the iAdvize Messenger Android SDK into your native Android mobile applications.

### ✨ Demo project

A demo project is available on [Github](https://github.com/iadvize/iadvize-android-sdk), almost all of the SDK code snippets used in this documentation can be found there in a real application context.

### 🆕 Latest SDK release

The latest Android SDK release is available on the same GitHub repository release page: [https://github.com/iadvize/iadvize-android-sdk/releases/latest](https://github.com/iadvize/iadvize-android-sdk/releases/latest).

> *⚠️ In the following snippets the SDK version is written as `x.y.z`, don’t forget to change it with the latest SDK version found at the above links.*

### 📔 API reference

The full Kotlin API reference can be found on the following link: [https://iadvize.github.io/iadvize-android-sdk/](https://iadvize.github.io/iadvize-android-sdk/).

### ⚙️ Setting up the SDK

#### 1️⃣ Adding the SDK dependency

Add the iAdvize repository to your project repositories inside your top-level Gradle build file:

<pre class="prettyprint">
// Project-level build.gradle.kts

allprojects {
  repositories {
    maven { url = uri("https://raw.github.com/iadvize/iadvize-android-sdk/master") }
  }
}
</pre>

Add the iAdvize Messenger SDK dependency inside your module-level Gradle build file:

<pre class="prettyprint">
// Module-level build.gradle.kts

configurations {
  all {
    exclude(group = "xpp3", module = "xpp3")
  }
}

dependencies {
  implementation("com.iadvize:iadvize-sdk:x.y.z")
}
</pre>

> *⚠️ The `exclude` configuration is required because the iAdvize Messenger SDK uses [Smack](https://github.com/igniterealtime/Smack), an XMPP library that is built upon `xpp3`, which is bundled by default in the Android framework. This exclude ensures that your app does not also bundle `xpp3` to avoid classes duplication errors.*

After syncing your project you should be able to import the iAdvize dependency in your application code with `import com.iadvize.conversation.sdk.IAdvizeSDK`

⌨️ **In-context example:**

- [Project-level Gradle file](https://github.com/iadvize/iadvize-android-sdk/blob/master/build.gradle.kts)
- [Module-level Gradle file](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/build.gradle.kts)
- [Import](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/App.kt#L5)


> *⚠️ From the version 2.5 and onward, the SDK supports video conversations using a third party native (C++) binaries. If you are delivering your app using an APK you will note a size increase as the default behavior of the build system is to include the binaries for each ABI in a single APK. We strongly recommended that you take advantage of either [App Bundles](https://developer.android.com/guide/app-bundle) or [APK Splits](https://developer.android.com/studio/build/configure-apk-splits) to reduce the size of your APKs while still maintaining maximum device compatibility.*

#### 2️⃣ Activating the SDK

Before activating the SDK, you will need to provide a reference to your application object and initiate the SDK with it.

In your `AndroidManifest.xml` declare your application class:

<pre class="prettyprint">
&lt;application
  android:name=&quot;my.app.package.App&quot;&gt;
  &lt;!-- your activities etc... --&gt;
&lt;/application&gt;
</pre>

This class should then initiate the SDK:

<pre class="prettyprint">
package my.app.package.App

class App : Application() {
  override fun onCreate() {
    super.onCreate()
    IAdvizeSDK.initiate(this)
  }
}
</pre>

After that you can activate the SDK using the `activate` function with your `projectId` (see the [Prerequisites](#⚙️-prerequisites) section to get that identifier). You have access to callbacks in order to know if the SDK has been successfully activated. In case of an SDK activation failure the callback will give you the reason of the failure and you may want to retry later:

<pre class="prettyprint">
IAdvizeSDK.activate(
  projectId = 0000,
  authenticationOption = AuthenticationOption.Simple("UserIdentifier"),
  gdprOption = GDPROption.Disabled,
  callback = object : IAdvizeSDK.Callback {
    override fun onSuccess() {
      Log.d("iAdvize SDK", "The SDK has been activated.")
    }
    override fun onFailure(t: Throwable) {
      Log.e("iAdvize SDK", "The SDK activation failed with:", t)
    }
  }
)
</pre>

⌨️ **In-context example:**

- [SDK Initiation](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/App.kt#L15)
- [SDK Activation](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/App.kt#L32)

###### Authentication modes

You can choose between multiple authentication options:

- **Anonymous**, when you have an unidentified user browsing your app: `AuthenticationOption.Anonymous`
- **Simple**, when you have a logged in user in your app. You must pass a unique string identifier so that the visitor will retrieve his conversation history across multiple devices and platforms: `AuthenticationOption.Simple("userId")`
- **Secured**: use it in conjunction with your in-house authentication system. You must pass a *JWE provider* callback that will be called when an authentication is required, you will then have to call your third party authentication system for a valid JWE to provide to the SDK:

<pre class="prettyprint">
AuthenticationOption.Secured(object : AuthenticationOption.JWEProvider {
  override fun onJWERequested(callback: AuthenticationOption.JWECallback) {
    // Fetch JWE from your own secure auth process
    callback.onJWERetrieved(jwe)
    // or callback.onJWEFailure(exception)
  }
})
</pre>

> *⚠️ For the __Simple__ authentication mode, the identifier that you pass must be __unique and non-discoverable for each different logged-in user__.*

Once the iAdvize Messenger SDK is successfully activated, you should see a success message in the console:

<pre class="prettyprint">
✅ iAdvize conversation activated, the version is x.y.z
</pre>

#### 3️⃣ Logging the user out

You will have to explicitly call the `logout` function of the iAdvize Messenger SDK when your user sign out of your app:

<pre class="prettyprint">
IAdvizeSDK.logout()
</pre>

#### 4️⃣ Displaying logs

To have more information on what’s happening on the SDK side you can change the log level and choose between:

<pre class="prettyprint">
VERBOSE
INFO
WARNING
ERROR
</pre>

To do so just add this line to your project:

<pre class="prettyprint">
IAdvizeSDK.logLevel = Logger.Level.VERBOSE
</pre>

### 💬 Starting a conversation

To be able to start a conversation you will first have to **trigger a targeting rule** in order for the default chat button to be displayed. The Chatbox will then be accessible by clicking on that chat button.

#### 1️⃣ Configuring the targeting language

The targeting rule configured in the iAdvize Administration Panel is setup for a given language.
This means that if, for example, you setup a targeting rule to be triggered only for `EN` users and your current user’s device is in `FR`, the targeting rule will not trigger.

By default, the targeting rule language used is the user’s device current language. You can force the targeting language to a specific value using:

<pre class="prettyprint">
IAdvizeSDK.targetingController.language = SDKLanguageOption.Custom(Language.FR)
</pre>

> *⚠️ This `language` property is __NOT__ intended to change the language displayed in the SDK. It is solely used for the targeting process purpose.*

#### 2️⃣ Activating a targeting rule

Using a targeting rule UUID (see the [Prerequisites](⚙️-prerequisites) section to get that identifier), you can engage a user by calling:

<pre class="prettyprint">
IAdvizeSDK.targetingController.activateTargetingRule(
  TargetingRule(
    targetingRuleUUID,
    ConversationChannel.CHAT // or ConversationChannel.VIDEO
  )
)
</pre>

If all the following conditions are met, the default chat button should appear:

- the targeting rule exists and is enabled in the administration panel
- the targeting rule language set in the SDK matches the language configured for this rule
- an operator assigned to this rule is available to answer (connected and with a free chat slot)

> *⚠️ After you activate a rule and it succeeds (by displaying the button), those conditions are checked every 30 seconds to verify that the button should still be displayed or not. At the first failure from this periodic check, the button is hidden and the SDK stops verifying the conditions. It means that if the rule cannot be triggered (after the first call, or after any successive check), you will have to call the `activateTargetingRule` (or `registerUserNavigation`) method again to restart the engagement process.*

#### 3️⃣ Initiating the conversation

Once the default chat button is displayed, the visitor tap on it to access the Chatbox. After composing and sending a message a new conversation should pop up in the operator desk.

![Chat button is displayed. Visitor composes a message & send it.](./assets/images/mobile-sdk/02-conv-start-mobile.png)
![Conversation appears in the operator desk](./assets/images/mobile-sdk/03-conv-start-desk.png)

#### 4️⃣ Following user navigation

While your user navigates through your app, you will have to update the active targeting rule in order to engage him/her with the best conversation partner at any time. In order to so, the SDK provides you with multiple navigation options to customize the behavior according to your needs:

<pre class="prettyprint">
// To clear the active targeting rule and thus stopping the engagement process (this is the default behavior)
val navOption = NavigationOption.ClearActiveRule

// To keep/start the engagement process with the same active targeting rule in the new user screen
val navOption = NavigationOption.KeepActiveRule

// To keep/start the engagement process but with another targeting rule for this screen
val navOption = NavigationOption.ActivateNewRule(newRule)

// Register the user navigation through your app
IAdvizeSDK.targetingController.registerUserNavigation(navOption)
</pre>

> *⚠️ Please note that calling `registerUserNavigation` with `NavigationOption.ClearActiveRule` will stop the engagement process, and calling it with other options will start it if it is stopped. Thus you may never use `activateTargetingRule` in your app and only rely on `registerUserNavigation` for your engagement process management.*

⌨️ **In-context example:** [Registering User Navigation](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/product/ProductDetailFragment.kt#L42)

### 👋 Configuring GDPR and welcome message

#### 1️⃣ Adding a welcome message

As seen above, the Chatbox is empty by default. You can configure a welcome message that will be displayed to the visitor when no conversation is ongoing.

<pre class="prettyprint">
val configuration = ChatboxConfiguration()
configuration.automaticMessage = "Any question? Say Hello to Smart and we will answer you as soon as possible! 😊"
IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

⌨️ **In-context example:** [Welcome message](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/IAdvizeSDKConfig.kt#L58)

When no conversation is ongoing, the welcome message is displayed to the visitor:

![When no conversation is ongoing, the welcome message is displayed to the visitor](./assets/images/mobile-sdk/04-welcome-message.png)

#### 2️⃣ Enabling GDPR approval

If you need to get the visitor consent on GDPR before he starts chatting, you can pass a `GDPROption` while activating the SDK. By default this option is set to `Disabled`.

If enabled, a message will request the visitor approval before allowing him to send a message to start the conversation:

![GDPR approval request](./assets/images/mobile-sdk/05-gdpr-approval.png)

This `GDPROption` dictates how the SDK behaves when the user taps on the `More information` button. You can either:

- provide an URL pointing to your GPDR policy, it will be opened on user click
- provide a listener/delegate, it will be called on user click and you can then implement your own custom behavior

> *⚠️ If your visitors have already consented to GDPR inside your application, you can activate the iAdvize SDK without the GDPR process. However, be careful to explicitly mention the iAdvize Chat part in your GDPR consent details.*

Let’s activate the iAdvize Messenger SDK using the first option:

<pre class="prettyprint">
val legalInfoUri = URI.create("http://yourlegalinformationurl.com/legal")
IAdvizeSDK.activate(
  projectId = projectId,
  authenticationOption = AuthenticationOption.Anonymous,
  gdprOption = GDPROption.Enabled(GDPREnabledOption.LegalUrl(legalInfoUri)),
  callback = sdkActivationCallback
)
</pre>

Just like the welcome message above, the GDPR message can also be configured via the `ChatboxConfiguration` object:

<pre class="prettyprint">
val configuration = ChatboxConfiguration()
configuration.automaticMessage = "Any question? Say Hello to Smart and we will answer you as soon as possible! 😊"
configuration.gdprMessage = "Your own GDPR message."
IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

⌨️ **In-context example:**

- [GDPR Option](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/IAdvizeSDKConfig.kt#L38)
- [GDPR Message](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/IAdvizeSDKConfig.kt#L60)

### 🎨 Branding the Chatbox

The `ChatboxConfiguration` object that we used in the previous section to customize the welcome and GDPR messages can also be used to change the Chatbox UI to better fit into the look and feel of your application.

#### 1️⃣ Changing the Chatbox color

You can setup a main color on the SDK which will be applied to:

- the send button in the Chatbox
- the blinking text cursor in the message input of the Chatbox
- the background of the visitor messages bubbles

<pre class="prettyprint">
val configuration = ChatboxConfiguration()
configuration.mainColor = Color.RED
IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

#### 2️⃣ Styling the navigation bar

Some parts of the he toolbar/navigationbar appearing at the top of the Chatbox can also be customized:

- the background color
- the main color
- the title

<pre class="prettyprint">
val configuration = ChatboxConfiguration()
configuration.toolbarBackgroundColor = Color.BLACK,
configuration.toolbarMainColor = COLOR.WHITE,
configuration.toolbarTitle = "Conversation"
IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

#### 3️⃣ Updating the font

The font used in the Chatbox can easily be updated using your own font:

<pre class="prettyprint">
val configuration = ChatboxConfiguration()
configuration.fontPath = "fonts/comic_sans_ms_regular.ttf"
IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

> *⚠️ The font should be placed inside the assets folder. Here the file is located at `src/main/assets/fonts/comic_sans_ms_regular.ttf`*

#### 4️⃣ Using a brand avatar

The operator avatar displayed alongside his messages can be updated for branding purposes. You can specify a drawable either via an URL or a local resource.

<pre class="prettyprint">
val configuration = ChatboxConfiguration()

// Update the incoming message avatar with a Drawable resource.
configuration.incomingMessageAvatar = IncomingMessageAvatar.Image(
  ContextCompat.getDrawable(context, R.drawable.ic_brand_avatar)
)

// Update the incoming message avatar with an URL.
configuration.incomingMessageAvatar = IncomingMessageAvatar.Url(URL("http://avatar.url"))

IAdvizeSDK.chatboxController.setupChatbox(configuration)
</pre>

> *⚠️ GIFs are not supported*

### 🎨 Branding the Default Floating Button

By default, the SDK uses its own Default Floating Button to the user to engage the conversation. This Default Floating Button display process is automated by the SDK and works out of the box. You have however limited possibilities to brand it to your needs.

The Default Floating Button can be parametrized, both in its look (colors / icon) and position (anchor / margins) using the appropriate configuration:

<pre class="prettyprint">
val configuration = DefaultFloatingButtonConfiguration(
  anchor = Gravity.START or Gravity.BOTTOM,
  margins = DefaultFloatingButtonMargins(),
  backgroundTint = ContextCompat.getColor(this, R.color.colorPrimary),
  iconResIds = mapOf(
    ConversationChannel.CHAT to R.drawable.chat_icon,
    ConversationChannel.VIDEO to R.drawable.video_icon
  )
  iconTint = Color.WHITE
)
val option = DefaultFloatingButtonOption.Enabled(configuration)
IAdvizeSDK.defaultFloatingButtonController.setupDefaultFloatingButton(option)
</pre>

⌨️ **In-context example:** [Default Floating Button Configuration](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/IAdvizeSDKConfig.kt#L43)

### ✨ Using a custom chat button

If you are not satisfied with the Default Floating Button look and feel or if you want to implement a specific behavior related to its display you may need to use a custom conversation button.

With a custom button it is your responsibility to:

- design the floating or fixed button to invite your user to chat
- hide/show the button following the active targeting rule availability and the ongoing conversation status
- open the Chatbox when the user presses your button

#### 1️⃣ Disabling the Default Floating Button

<pre class="prettyprint">
IAdvizeSDK.defaultFloatingButtonController.setupDefaultFloatingButton(DefaultFloatingButtonOption.Disabled)
</pre>

#### 2️⃣ Displaying/hiding the chat button

The chat button is linked to the targeting and conversation workflow and should update its visibility each time the status of those workflows is changed.
First of all you need to implement the appropriate callbacks:

<pre class="prettyprint">
IAdvizeSDK.targetingController.listeners.add(object : TargetingListener {
  override fun onActiveTargetingRuleAvailabilityUpdated(isActiveTargetingRuleAvailable: Boolean) {
    // SDK active rule availability changed to isActiveTargetingRuleAvailable
    updateChatButtonVisibility()
  }
})

IAdvizeSDK.conversationController.listeners.add(object : ConversationListener {
  override fun onOngoingConversationUpdated(ongoingConversation: OngoingConversation?) {
    // SDK ongoing conversation has updated
    updateChatButtonVisibility()
  }
  override fun onNewMessageReceived(content: String) {
    // A new message was received via the SDK
  }
  override fun handleClickedUrl(uri: Uri): Boolean {
    // A message link was tapped, return true if you want your app to handle it
    return false
  }
})
</pre>

The chat button gives access to the Chatbox so it should be visible:

- at all times when a conversation is ongoing to allow the visitor to come back to the current conversation
- when the active targeting rule is available, to engage the visitor to chat

<pre class="prettyprint">
fun updateChatButtonVisibility() {
  val sdkActivated = IAdvizeSDK.activationStatus == IAdvizeSDK.ActivationStatus.ACTIVATED
  val chatboxOpened = IAdvizeSDK.chatboxController.isChatboxPresented()
  val ruleAvailable = IAdvizeSDK.targetingController.isActiveTargetingRuleAvailable()
  val hasOngoingConv = IAdvizeSDK.conversationController.ongoingConversation() != null

  if (sdkActivated && !chatboxOpened && (hasOngoingConv || ruleAvailable)) {
    showChatButton()
  } else {
    hideChatButton()
  }
}
</pre>

#### 3️⃣ Opening the Chatbox

When the visitor taps on your custom chat button you should open the Chatbox by calling the following method:

<pre class="prettyprint">
IAdvizeSDK.chatboxController.presentChatbox(context)
</pre>

⌨️ **In-context example:** [Full custom chat button implementation](https://gist.github.com/Judas/d0a34a50f1b6b8d542d77af5db9d9787)

### 🔔 Handling push notifications

> *⚠️ Before starting this part you will need to configure push notifications inside your application. You can refer to the following resources if needed: [Firebase Cloud Messaging documentation](https://firebase.google.com/docs/cloud-messaging/android/client). You will also need to ensure that the push notifications are setup in your iAdvize project. The process is described in the [SDK Knowledge Base](https://help.iadvize.com/hc/en-gb/articles/360019839480).*

#### 1️⃣ Registering the device token

For the SDK to be able to send notifications to the visitor’s device, its unique `device push token` must be registered:

<pre class="prettyprint">
class NotificationService : FirebaseMessagingService() {
  override fun onNewToken(token: String) {
    super.onNewToken(token)
    IAdvizeSDK.notificationController.registerPushToken(token)
  }
}
</pre>

⌨️ **In-context example:** [Device token register](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/notifications/NotificationService.kt#L55)

#### 2️⃣ Enabling/disabling push notifications

Push notifications are activated as long as you have setup the push notifications information for your app on the iAdvize administration website (process is described in the [SDK Knowledge Base](https://help.iadvize.com/hc/en-gb/articles/360019839480)). You can manually enable/disable them at any time using:

<pre class="prettyprint">
IAdvizeSDK.notificationController.enablePushNotifications(object : IAdvizeSDK.Callback {
  override fun onSuccess() {
    // Enable succeded
  }
  override fun onFailure(t: Throwable) {
    // Enable failed
  }
})

IAdvizeSDK.notificationController.disablePushNotifications(object : IAdvizeSDK.Callback {
  override fun onSuccess() {
    // Disable succeded
  }
  override fun onFailure(t: Throwable) {
    // Disable failed
  }
})
</pre>

#### 3️⃣ Handling push notifications reception

Once setup, you will receive push notifications when the operator sends any message. As the SDK notifications are caught in the same place than your app other notifications, you first have to distinguish if the received notification comes from iAdvize or not. This can be done using:

<pre class="prettyprint">
class NotificationService : FirebaseMessagingService() {
  override fun onMessageReceived(remoteMessage: RemoteMessage) {
    if (IAdvizeSDK.notificationController.isIAdvizePushNotification(remoteMessage.data)) {
      // This is an iAdvize SDK notification
    }
  }
}
</pre>

> *⚠️ Notifications will be received in your app for all messages sent by the agent. It is your responsability to display the notification and to check wether or not it is relevant to display it. For instance you don’t need to show a notification to the visitor when the Chatbox is opened:*

<pre class="prettyprint">
fun shouldDisplayNotification(remoteMessage: RemoteMessage) =
  IAdvizeSDK.notificationController.isIAdvizePushNotification(remoteMessage.data) 
  && !IAdvizeSDK.chatboxController.isChatboxPresented()
</pre>

#### 4️⃣ Customizing the notification

You are responsible for displaying the notification so you can use any title / text / icon you want.
The text sent by the agent is available in the `content` part of the notification data received.

<pre class="prettyprint">
override fun onMessageReceived(remoteMessage: RemoteMessage) {
  if (IAdvizeSDK.notificationController.isIAdvizePushNotification(remoteMessage.data)) {
    val agentMessageReceived = remoteMessage.data["content"] ?: "Default text"
  }
}
</pre>

⌨️ **In-context example:** [Handling received notification](https://github.com/iadvize/iadvize-android-sdk/blob/master/mobile/src/main/java/com/iadvize/conversation/sdk/demo/feature/notifications/NotificationService.kt#L68)

### 📈 Adding value to the conversation

#### 1️⃣ Registering visitor transactions

You can register a transaction made within your application:

<pre class="prettyprint">
IAdvizeSDK.transactionController.register(
  Transaction(
    "transactionId",
    Date(),
    10.00,
    Currency.EUR
  )
)
</pre>

#### 2️⃣ Saving visitor custom data

The iAdvize Messenger SDK allows you to save data related to the visitor conversation:

<pre class="prettyprint">
IAdvizeSDK.visitorController.registerCustomData(listOf(
  CustomData.fromString("Test", "Test"),
  CustomData.fromBoolean("Test2", false),
  CustomData.fromDouble("Test3", 2.0),
  CustomData.fromInt("Test4", 3)
),
object : IAdvizeSDK.Callback {
  override fun onSuccess() {
    // Success
  }
  override fun onFailure(t: Throwable) {
    // Failure
  }
})
</pre>

> *⚠️ As those data are related to the conversation they cannot be sent if there is no ongoing conversation. Custom data registered before the start of a conversation are stored and the SDK automatically tries to send them when the conversation starts.*

The visitor data you registered are displayed in the iAdvize Operator Desk in the conversation sidebar, in a tab labelled  `Custom data`:

![Custom data tab shows registered data from the SDK](./assets/images/mobile-sdk/06-custom-data.png)

### 👍 Fetching visitor satisfaction

From SDK version `2.4.0` and onward, the satisfaction survey is automatically sent to the visitor at the end of the conversation, as long as it is activated in the iAdvize administration website.
The survey is presented to the visitor in a conversational approach, directly into the Chatbox.

<img src="./assets/images/mobile-sdk/07-satisfaction-survey.gif" alt="Satisfaction survey" style="display: block; width: 20%; height: auto;" />

> *⚠️ Only the `CSAT`, `NPS` and `COMMENT` steps of the survey are supported.*

### 🚦 Testing the SDK

If you are running unit tests that implies the SDK, some additional steps may be needed.

The Android SDK uses two device system constants that are not instantiated inside unit test flow, you will have to register them inside your unit tests initiation:

<pre class="prettyprint">
ReflectionHelpers.setStaticField(android.os.Build::class.java, "MODEL", "whatever")
ReflectionHelpers.setStaticField(android.os.Build::class.java, "MANUFACTURER", "whatever")
</pre>

Please also be sure to initiate the SDK during the unit tests setup (see the [Setting up the SDK](#⚙️-setting-up-the-sdk) section above).


## iOS

### ✨ Demo project
TODO

## ReactNative

## Flutter