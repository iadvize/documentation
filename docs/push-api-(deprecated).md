
# Push API (deprecated)

The iAdvize Push API will be deprecated starting september, 2017. The Push API will stop working from january 30th, 2018. From now, we recommend to use our webhooks system.
The Push API allows data to be pushed to URI callbacks when an event is fired.  
The Push API uses JSON exclusively. XML is not supported. Push requests are sent with a POST method.

## Events

### operator.login

When an operator connects to the desk.

**Returned data**

<pre class="prettyprint lang-js">{
    "name": "operator.login",
    "datetime": {
        "created": "2014-01-01 00:00:00",
        "sent": "2014-01-01 00:00:01"
    },
    "parameters": {
        "operator_id": 1
    }
}
</pre>

### operator.logout

When an operator disconnects from the desk.

**Returned data**

<pre class="prettyprint lang-js">{
    "name": "operator.logout",
    "datetime": {
        "created": "2014-01-01 00:00:00",
        "sent": "2014-01-01 00:00:01"
    },
    "parameters": {
        "operator_id": 1
    }
}
</pre>

### conversation.start

When a conversation is started.

**Returned data**

<pre class="prettyprint lang-js">{
    "name": "conversation.start",
    "datetime": {
        "created": "2014-01-01 00:00:00",
        "sent": "2014-01-01 00:00:01"
    },
    "parameters": {
        "conversation_id": 1,
        "type":            "chat|call|video",
        "operator_id":     1,
        "website_id":      1,
        "group_id":        1,
        "custom_data":     {
            "example":     "value"
        }
    }
}
</pre>

### conversation.end

When a conversation is ended by the operator.

**Returned data**

<pre class="prettyprint lang-js"> {
    "name": "conversation.end",
    "datetime": {
        "created": "2014-01-01 00:00:00",
        "sent": "2014-01-01 00:00:01"
    },
    "parameters": {
        "conversation_id": 1,
        "type":            "chat|call|video",
        "operator_id":     1,
        "website_id":      1,
        "group_id":        1
    }
}
</pre>
