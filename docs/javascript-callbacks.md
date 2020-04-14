# Javascript Callbacks

iAdvize provides Javascript callbacks functions that can be used to perform actions on specific events.

## How to use callbacks

To execute custom code during an iAdvize callback function you have to define an `iAdvizeCallbacks` variable that will contain the callbacks you want to use.

**⚠️ Please note that you must declare this variable before the main iAdvize tag.**

Each callback function has an `obj` variable passed as a parameter that could contain some extra information about iAdvize elements.

In the example bellow we want to track Google Analytics events when a chat or a call starts / ends :

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
  //iAdvize callback functions are listed here
  onChatStarted: function(obj){
    // Chat session starts
    _gaq.push(['_trackEvent', 'iAdvize', 'Chat Start', obj.startedBy]);
  },
  onChatEnded: function(obj){
    // Chat session ends
    _gaq.push(['_trackEvent', 'iAdvize', 'Chat End', obj.startedBy]);
  },
  onCallStarted: function(obj){
    // Call session starts
    _gaq.push(['_trackEvent', 'iAdvize', 'Call Start']);
  },
  onCallEnded: function(obj){
    // Call session ends
    _gaq.push(['_trackEvent', 'iAdvize', 'Call End']);
  }
};
//Put you iAdvize tracking code below...
</pre>

## Callbacks Index

### onChatDisplayed

- Called when : a chat popin is displayed on the visitor screen **(either opened or reduced)**.
- Parameter(s) : `obj` is null

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onChatDisplayed: function(obj){
        // Chat window is displayed
        ...
    }
};
</pre>

### onChatButtonDisplayed

- Called when : a click to chat button is displayed on the visitor screen.
- Parameter(s) : `obj` is null

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onChatButtonDisplayed: function(obj){
        // Chat button is displayed
        ...
    }
};
</pre>

### onChatStarted

- Called when : a chat discussion has started.
- Parameter(s) : `obj` contain 2 values:
  - `obj.id` -> Chat identifier that you can use with our REST API
  - `obj.conversationId` -> Conversation UUID that you can use with our GraphQL API
  - `obj.vuid` -> Visitor Unique Id is a random string which can be used for analytics purposes

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onChatStarted: function(obj){
        // Chat is started
        console.log('chat #' +obj.id + ' was started');
    }
};
</pre>

### onChatEnded

- Called when : a chat discussion has ended.
- Parameter(s) : `obj` contain 2 values:
  - `obj.id` -> Chat identifier
  - `obj.endedBy` -> Who ended the chat ('operator' or 'visitor')

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onChatEnded: function(obj){
        // Chat discussion is ended
        ...
    }
};
</pre>

### onCallButtonDisplayed

- Called when : a click to call button is displayed on the visitor screen.
- Parameter(s) : `obj` is null

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onCallButtonDisplayed: function(obj){
        // Call button is displayed
        ...
    }
};
</pre>

### onMessageReceived

- Called when : an operator message is received by the visitor.
- Parameter(s) : `obj` contain 4 values:
  - `obj.time` -> local time of the message (visitor time)
  - `obj.msg` -> the message itself
  - `obj.date` -> local datetime of the message ([ISO 8601](https://www.w3.org/TR/NOTE-datetime))
  - `obj.operator` -> (optional) operator information if available
    - `obj.operator.id` -> iAdvize operator id
    - `obj.operator.externalId` -> operator external id or null if not provided in iAdvize admin 

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onMessageReceived: function(obj){
        // operator message received
        console.log('[' + obj.time + '] operator message: ' +obj.msg);
    }
};
</pre>

### onMessageSent

- Called when : the visitor sends a message.
- Parameter(s) : `obj` contain 2 values:
  - `obj.time` -> local time of the message (visitor time)
  - `obj.msg` -> the message itself

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onMessageSent: function(obj){
        // operator message received
        console.log('[' + obj.time + '] visitor message: ' +obj.msg);
    }
};
</pre>


### onSatisfactionDisplayed

- Called when : the satisfaction survey is displayed to the visitor.
- Parameter(s) : none

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onSatisfactionDisplayed: function(){
        // operator message received
        console.log('satisfaction survey displayed');
    }
};
</pre>

### onSatisfactionAnswered

- Called when : the visitor answers the satisfaction survey.
- Parameter(s) : `obj` is null

<pre class="prettyprint lang-js">var iAdvizeCallbacks = {
    onSatisfactionAnswered: function(obj){
        // operator message received
        console.log('visitor answered satisfaction survey');
    }
};
</pre>
