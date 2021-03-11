# Webhooks
## Introduction
When an event occurs, an HTTP `POST` call is issued on the callback urls you set up with the event data.
Data is sent with `application/json` header content-type, and `json` format as payload.
Callback urls must be defined with HTTPS protocol and should be available with `POST` verb to send data payload.
iAdvize expect to have à 20x http status in callback result.

## Subscribe to your first webhook
In order to subscribe to the webhooks of your website, you need to create an app in our marketplace.
You'll need to have a developer account that you can get by signing up on [this page](https://developers.iadvize.com/login).
You'll then be able to subscribe to all the available webhooks through our webhook building interface:
![iAdvize](./assets/images/Webhook_creation_interface.png).


## Conversation events description
| Name | Channel | Description | Comment |
| --- | --- | --- | --- | 
| `conversation.started` |`CALL`| Beginning of a call conversation | - 
| `v2.conversation.pushed` |`CHAT`,`VIDEO`| Beginning of a chat conversation or receiving of a conversation transferred by another operator. | Replace the use of old deprecated events (conversation.started and conversation.transferred)
| `v2.conversation.closed` | Onsite: `CHAT`, `CALL`, `VIDEO`<br /> Offsite: `FACEBOOK`, `FACEBOOK_BUSINESS_ON_MESSENGER`, `TWITTER`, `MOBILE_APP`, `SMS` | End of a conversation. <br />Conversations on offsite channels are automatically closed after 7 days of inactivity | Replace the use of old deprecated event (conversation.closed)
| `visitor.updated` | | Visitor information updated from desk or admin view | |

### Examples of payload for conversation events
**Output examples of Conversations domain:**

Please note :

| Attribute | Description |
| --- | --- |
| clientId | As a client of iAdvize you have a specific ID, it is what this one represents |
| visitorId | Each visitor has a unique ID. iAdvize calls it visitor unique ID |

#### conversation.started (only for call channel)

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "conversation.started",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 1,
    "operatorId": 1,
    "channel": "call",
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### visitor.updated

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "visitor.updated",
    "platform": "sd",
    "clientId": 1,
    "operatorId": 1,
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>


We are currently migrating our events to a new format to offer you more flexibility in the way you can query our data. 
With V2 events, you can query the corresponding resources through our [GraphQL api](#graphql-api-alpha).

### Payload examples of v2 conversation events

#### v2.conversation.pushed

<pre class="prettyprint lang-js">{
  "eventId": "0f0bb3af-5035-4ba3-b3fb-ff4879a3a74d",
  "eventType": "v2.conversation.pushed",
  "platform": "ha",
  "projectId": 1549,
  "clientId": 335,
  "conversationId": "4c8c7408-f73c-42cd-89e9-afbbee7d9024",
  "operatorId": 15253,
  "visitorExternalId": "63429889",
  "channel": "CHAT",
  "createdAt": "2019-04-12T07:58:35.171Z",
  "sentAt": "2019-04-12T07:58:35.496Z"
}
</pre>

#### v2.conversation.closed

<pre class="prettyprint lang-js">{
  "eventId": "0f0bb3af-5035-4ba3-b3fb-ff4879a3a74d",
  "eventType": "v2.conversation.closed",
  "platform": "ha",
  "projectId": 1549,
  "clientId": 335,
  "conversationId": "4c8c7408-f73c-42cd-89e9-afbbee7d9024",
  "operatorIds": [
    15253,
    15254
   ],
  "visitorExternalId": "63429889", //or null for offsite channels such as Facebook
  "channel": "CHAT",
  "createdAt": "2019-04-12T07:58:35.171Z",
  "sentAt": "2019-04-12T07:58:35.496Z"
}
</pre>

### Deprecated conversation events

`WARNING`: the following events should not be used anymore, they still appear in this documentation only for history purposes!

#### ~~conversation.started for channel chat~~

PLEASE DO NOT USE (refer to warning above).

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "conversation.started",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 1,
    "operatorId": 1,
    "channel": "chat",
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### ~~conversation.transferred ~~

PLEASE DO NOT USE (refer to warning above).

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "conversation.transferred",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 2,
    "transferredConversationId": 1,
    "operatorId": 1,
    "channel": "chat",
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### ~~conversation.closed ~~

PLEASE DO NOT USE (refer to warning above).

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "conversation.closed",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 1,
    "operatorId": 1,
    "channel": "chat",
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

## User events description

| Domain | Name |
| --- | --- |
| `user.created` | User created |
| `user.updated` | User information updated |
| `satisfaction.answered` | |
| `user.connected` | |
| `user.disconnected` | |


### Payloads
#### user.created
<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "user.created",
    "platform": "sd",
    "clientId": 1,
    "userId": 1,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### user.updated
<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "user.updated",
    "platform": "sd",
    "clientId": 1,
    "userId": 1,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### satisfaction.answered

##### Example with `customerSatisfaction` filled

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "satisfaction.answered",
    "platform": "sd",
    "projectId": 3030,
    "clientId": 1,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00",
    "conversationId": "d36cd3c4-2d16-4a77-97c2-620bde859b40",
    "customerSatisfaction" : 3
}
</pre>

##### Example with `netPromoterScore` filled

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "satisfaction.answered",
    "platform": "sd",
    "projectId": 3030,
    "clientId": 1,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00",
    "conversationId": "d36cd3c4-2d16-4a77-97c2-620bde859b40",
    "netPromoterScore" : 3
}
</pre>

##### Example with `satisfactionComment` filled

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "satisfaction.answered",
    "platform": "sd",
    "projectId": 3030,
    "clientId": 1,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00",
    "conversationId": "d36cd3c4-2d16-4a77-97c2-620bde859b40",
    "satisfactionComment" : "It was very helpful"
}
</pre>

##### HTTP stack trace example for “conversation.closed” event

`POST /webhook HTTP/1.1`

<pre class="prettyprint lang-js">
Host: localhost
X-iAdvize-Signature: sha256=110e8400-e29b-11d4-a716-446655440000
X-iAdvize-CorrelationId: 332e8400-e34b-11d4-a716-446655444444
X-iAdvize-Delivery: 110e8400-e29b-11d4-a716-446655440000
Content-Type: application/json
Content-Length: 3442

{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "conversation.closed",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 1,
    "operatorId": 1,
    "channel": "chat",
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

### Deprecated user events

`WARNING`: the following events should not be used anymore, they still appear in this documentation only for history purposes!

#### ~~satisfaction.filled~~

PLEASE DO NOT USE (refer to warning above).

<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "satisfaction.filled",
    "platform": "sd",
    "websiteId": 1,
    "clientId": 1,
    "conversationId": 1,
    "operatorId": 2,
    "visitorId": "593de0891b628a50b09835dc6c0e92565329c74baa90e",
    "score": 3,
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

## Delivery headers
iAdvize will send payload with three additional headers:

* X-iAdvize-Delivery: UUID, unique identifier to describe this webhook delivery
* X-iAdvize-CorrelationId: UUID, event identifier used in retry webhooks to track same callback calls.
* X-iAdvize-Signature: Hash signature, cf. Security section

## Webhook retry management

If errors occur during webhook query (40x, 50x http status codes), we will retry two times.
We will try to send you the following requests:
* First time after delay of 10 seconds,
* and second time after 20 seconds (so, 30 seconds after first call).

In case of failure, you may need to track events in error, by following "X-iAdvize-CorrelationId" in headers, or "eventId" in payload.

## Webhook security

Please refer to [this section](/documentation/build-apps#app-security).
