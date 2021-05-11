# Javascript Callbacks

## Overview <span hidden>callbacks</span>

### Introduction

iAdvize provides Javascript callbacks functions that can be used to perform actions on specific events.

Some callbacks have a parameter that contains data specific to the triggered event.

### How to use callbacks

To execute custom code during an iAdvize callback function you have to define the callbacks you want to use in a `window.iAdvizeCallbacks` object.

**⚠️ Please note that the `window.iAdvizeCallbacks` must be defined before the main iAdvize tag.**

---

## Reference <span hidden>callbacks</span>

| Callback name             | Description                                                                                   |
| ------------------------- | --------------------------------------------------------------------------------------------- |
| [onChatDisplayed](/documentation/javascript-callbacks#onchatdisplayed)         | Triggered when the chatbox is displayed on the visitor screen **(either opened or reduced)**. |
| [onChatHidden](/documentation/javascript-callbacks#onchathidden)         | Triggered when the visitor closes the chatbox (after the conversation has been closed by the operator). |
| [onChatButtonDisplayed](/documentation/javascript-callbacks#onchatbuttondisplayed)   | Triggered when a “click to chat” button is displayed on the visitor screen.                   |
| [onChatStarted](/documentation/javascript-callbacks#onchatstarted)           | Triggered when a chat conversation has started.                                               |
| [onChatEnded](/documentation/javascript-callbacks#onchatended)             | Triggered when a chat conversation has ended.                                                 |
| [onCallButtonDisplayed](/documentation/javascript-callbacks#oncallbuttondisplayed)   | Triggered when a “click to call” button is displayed on the visitor screen.                   |
| [onMessageReceived](/documentation/javascript-callbacks#onmessagereceived)       | Triggered when an operator message is received by the visitor.                                |
| [onMessageSent](/documentation/javascript-callbacks#onmessagesent)           | Triggered when the visitor sends a message.                                                   |
| [onSatisfactionDisplayed](/documentation/javascript-callbacks#onsatisfactiondisplayed) | Triggered when the satisfaction survey is displayed to the visitor.                           |
| [onSatisfactionAnswered](/documentation/javascript-callbacks#onsatisfactionanswered)  | Triggered when the visitor has answered all the questions in the satisfaction survey.                                   |

### onChatDisplayed

Triggered when the chat window is displayed on the visitor screen **(either opened or reduced)**.

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onChatDisplayed = function() {
  // Chat window is displayed
  ...
};
</pre>

### onChatHidden

Triggered when the visitor closes the chatbox (after the conversation has been closed by the operator).

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onChatHidden = function() {
  // Chat window is hidden
  ...
};
</pre>

### onChatButtonDisplayed

Triggered when a “click to chat” button is displayed on the visitor screen.

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onChatButtonDisplayed = function() {
  // Chat button is displayed
  ...
};
</pre>

### onChatStarted

Triggered when a chat conversation has started.

#### Context parameter:

| Property                 | Description                                                                   |
| ------------------------ | ----------------------------------------------------------------------------- |
| `context.id`             | Legacy conversation ID (integer ID)                                           |
| `context.conversationId` | New conversation ID in UUID format that you can use in our GraphQL API        |
| `context.vuid`           | Visitor Unique Id is a random string which can be used for analytics purposes |

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onChatStarted = function(context) {
  // Chat is started
  ...
};
</pre>

### onChatEnded

Triggered when a chat conversation has ended.

#### Context parameter:

| Property                 | Description                                                                   |
| ------------------------ | ----------------------------------------------------------------------------- |
| `context.id`             | Legacy conversation ID (integer ID)                                           |
| `context.endedBy`        | **⚠️ DEPRECATED.** The conversation can only be ended by an operator           |
| `context.conversationId` | New conversation ID in UUID format that you can use in our GraphQL API        |
| `context.vuid`           | Visitor Unique Id is a random string which can be used for analytics purposes |

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onChatEnded = function(context) {
  // Chat conversation is closed
  ...
};
</pre>

### onCallButtonDisplayed

Triggered when a “click to call” button is displayed on the visitor screen.

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onCallButtonDisplayed = function() {
  // Call button is displayed
  ...
};
</pre>

### onMessageReceived

Triggered when an operator message is received by the visitor.

#### Context parameter:

| Property                      | Description                                                                     |
| ----------------------------- | ------------------------------------------------------------------------------- |
| `context.time`                | Local time of the message (visitor time)                                        |
| `context.msg`                 | The text message received                                                       |
| `context.date`                | Local DateTime of the message ([ISO 8601](https://www.w3.org/TR/NOTE-datetime)) |
| `context.operator.id`         | Internal iAdvize operator id                                                    |
| `context.operator.externalId` | The operator external id provided by the customer                               |

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onMessageReceived = function(context) {
  // Operator message received
  ...
};
</pre>

### onMessageSent

Triggered when the visitor sends a message.

#### Context parameter:

| Property       | Description                              |
| -------------- | ---------------------------------------- |
| `context.time` | Local time of the message (visitor time) |
| `context.msg`  | The text message received                |

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onMessageSent = function(context) {
  // Visitor message sent
  ...
};
</pre>

### onSatisfactionDisplayed

Triggered when the satisfaction survey is displayed to the visitor.

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onSatisfactionDisplayed = function() {
  // Satisfaction survey displayed to the visitor
  ...
};
</pre>

### onSatisfactionAnswered

Triggered when the visitor has answered all the questions in the satisfaction survey.

#### Example:

<pre class="prettyprint lang-js">
window.iAdvizeCallbacks.onSatisfactionAnswered = function() {
  // Satisfaction survey answered by the visitor
  ...
};
</pre>

---

## Guides <span hidden>callbacks</span>

### Safely adds events in `window.iAdvizeCallbacks` object

If you need to add callbacks in different places in your code and to prevent overriding a previous callback definition, you should always use this line before adding your callbacks:

<pre class="prettyprint lang-js">
// Used to prevent overriding a previous definition
window.iAdvizeCallbacks = window.iAdvizeCallbacks || {};
</pre>

### Safely define a function for an event

If your code is splitted in multiple files or module, you may need to define several functions for the same event.

Here is a solution to avoid overwriting a previous function:

<pre class="prettyprint lang-js">
// Used to prevent overriding a previous definition
window.iAdvizeCallbacks = window.iAdvizeCallbacks || {};

var tempOnChatStarted = window.iAdvizeCallbacks.onChatStarted || function(){};
window.iAdvizeCallbacks.onChatStarted = function(context) {

  // Call the possible already defined callback
  tempOnChatStarted(context);

  // Your new custom code here
  // ...

};
</pre>

### Track some Google Analytics events

<pre class="prettyprint lang-js">
// Used to prevent overriding a previous definition
window.iAdvizeCallbacks = window.iAdvizeCallbacks || {};

// Chat session starts
window.iAdvizeCallbacks.onChatStarted = function(context) {
  _gaq.push(['_trackEvent', 'iAdvize', 'Chat Start', context.startedBy]);
};

// Chat session ends
window.iAdvizeCallbacks.onChatEnded = function(context) {
  _gaq.push(['_trackEvent', 'iAdvize', 'Chat End', context.startedBy]);
};

// Call session starts
window.iAdvizeCallbacks.onCallStarted = function() {
  _gaq.push(['_trackEvent', 'iAdvize', 'Call Start']);
};

// Call session ends
window.iAdvizeCallbacks.onCallEnded = function() {
  _gaq.push(['_trackEvent', 'iAdvize', 'Call End']);
};
</pre>
