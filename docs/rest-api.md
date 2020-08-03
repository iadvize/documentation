# REST API
**Current version:** 2.0

This API provides access and basic CRUD operations (create, read, update, delete) for the resources described in the documentation.
The REST API uses JSON exclusively. XML is not supported.

## Base URL

All URLs referenced in the documentation have the following base:

| Standard platform | High availability platform |
| --- | --- |
| `https://www.iadvize.com/api/2` | `https://ha.iadvize.com/api/2` |

The iAdvize REST API is served over HTTPS.

## Authentication

The API key must be attached to each request. You can use it in one of the following ways:

*   Passed in as a `X-API-Key` HTTP header
*   Passed in as a `key` GET parameter
*   Passed in as the username <small>(with an arbitrary password)</small> via `HTTP Basic authentication`

## Calls, errors & responses

### Authentication failed

<pre class="prettyprint lang-js">{
  meta: {
    status: "error",
    message: "Forbidden"
  }
}
</pre>

### Create

##### `POST /my_resource my_field=my_value`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    my_field: "my_value",
    _link: "/my_resource/123"
  }
}
</pre>

##### `POST /my_resource my_field=my_value` (with error)

<pre class="prettyprint lang-js">{
  meta: {
    status: "fail",
    message: "Field 'my_field_2' is missing.",
  }
}
</pre>

### Read

##### `GET /my_resource`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: [
    {
      id: 789,
      _link: "/my_resource/789"
    },
    {
      id: 456,
      _link: "/my_resource/456"
    },
    {
      id: 123,
      _link: "/my_resource/123"
    }
  ],
  pagination: {
    page: 1,
    pages: 1,
    limit: 20,
    count: 3
  }
}
</pre>

**Common filters**

| Filter | Description | Values |
| --- | --- | --- |
| page | Page number | `?page=1` |
| limit | Maximum number of resources per page (maximum possible value is 100) | `?limit=1` |
| full | Show all fields of the resource | `?full=1` |

Use the `*` character to broaden the scope of your search. E.g.: `filters[name]=*uli*`

##### `GET /my_resource/123`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    my_field: "my_value",
    _link: "/my_resource/123"
  }
}
</pre>

##### `GET /my_resource/456` (with error)

<pre class="prettyprint lang-js">{
  meta: {
    status: "fail",
    message: "Unknown 'my_resource' with 'id' 456."
  }
}
</pre>

### Update

##### `PUT /my_resource/123 my_field=my_new_value`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    my_field: "my_new_value",
    _link: "/my_resource/123"
  }
}
</pre>

##### `PUT /my_resource/123 my_field=my_value` (with error)

<pre class="prettyprint lang-js">{
  meta: {
    status: "fail",
    message: "Value of field 'my_field' is not valid."
  }
}
</pre>

### Delete

##### `DELETE /my_resource/123`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  }
}</pre>

##### `DELETE /my_resource/456` (with error)

<pre class="prettyprint lang-js">{
  meta: {
    status: "fail"
    message: "Unknown 'my_resource' with 'id' 456"
  }
}
</pre>

## Resources

### ~~Client~~ deprecated

⚠️ **This resource is deprecated.** You should consider using our GraphQL API with the `client` object

#### List all clients

`GET /client`

See below to discover used fields and see [reading section](#read) to discover some output examples.

This list is displayed depending on the rights of your API key.

#### Showing client

`GET /client/1`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Identifier | Integer |
| lang | Language | String (2 chars) |
| premium_enabled | The client has access to premium features | Boolean |

### ~~Website~~ deprecated

⚠️ **This resource is deprecated.** You should consider using our GraphQL API with the `project` or `projects` objects

#### List all your websites

`GET /website`

See below to discover used fields and see [reading section](#read) to discover some output examples.

#### Get a website details

`GET /website/1`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Identifier | Integer |
| url | URL | String |
| label | Label | String |
| client_id | Client identifier | Integer |
| currency | Currency | String |
| language_admin | Admin language | `en`, `de`, `es`, `it`, `pt`, `nl`, `se`, `tw`, `ja`, `ko` or `fr` |
| timezone | Timezone | String |

#### Update a website

`PUT /website/1`

See [updating section](#update) to discover some output examples.

### Operator

#### List your operators

`GET /operator`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| id | Operator identifier | | `?filters[id]=123` |
| group_id | Group identifier | | `?filters[group_id]=123` |
| website_id | Website identifier | | `?filters[website_id]=123` |
| website_list | Website identifiers | | `?filters[website_list]=1,2,3` |
| skill_id | Skill identifier | | `?filters[skill_id]=123` |
| name | Operator name | | `?filters[name]=genius` |
| external_id | External identifier | | `?filters[external_id]=MyExternalId` |

#### Get operator's details

`GET /operator/1`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Operator identifier | Integer |
| name | Name | String |
| first_name | First name | String |
| pseudo | Pseudonym | String |
| email | Email | Valid email |
| external_id | Your id if provided | String |
| role `deprecated, use roles property instead` | Role | `operator`, `manager` or `admin` |
| roles | Roles | List of string `expert`, `operator`, `manager` or `admin` |
| chat_enabled | Ability to process chat | Boolean |
| call_enabled | Ability to process call | Boolean |
| video_enabled | Ability to process video | Boolean |
| chat_max_number | Max. amount of chats an operator can process at the same time | Integer |
| chat_and_call | Ability to process chat and call simultaneously | Boolean |
| chat_priority | Chat priority of the operator | `0` or `10` |
| call_priority | Call priority of the operator | `0` or `10` |
| video_priority | Video priority of the operator | `0` or `10` |
| language_list | List of languages the operator can process | List of ISO2 (e.g. en, fr...) |
| language_admin | Admin language | `de`, `en`, `es` or `fr` |
| group_id | Group identifier | Integer |
| website_list | Website list identifiers | List of integer |
| skill_list | Skill list identifiers | List of integer |
| sso_key | [SSO token](/documentation/single-sign-on#single-sign-on) | String |

#### Create an operator

`POST /operator`

See [creating section](#create) to discover some output examples.

#### Update an operator

`PUT /operator/1`

See [updating section](#update) to discover some output examples.

#### Delete an operator

`DELETE /operator/1`

See [deleting section](#responses-delete) to discover some output examples.

#### Get operators live availability
Get the live availability of all of your operators.

`GET /operator/live`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: [
    {
      id: 456,
      connected: true,
      chat: {
        enabled: true,
        slot_number: 2,
        slot_max_number: 4,
        busy: false,
        available: true
      },
      call: {
        enabled: false,
        slot_number: 0,
        slot_max_number: 1,
        busy: false,
        available: false
      },
      video: {
        enabled: false,
        slot_number: 0,
        slot_max_number: 1,
        busy: false,
        available: false
      }
    }
  ]
}
</pre>

You can use previous filters.
*   In order to have more accurate results, only available operators are displayed in the default view.
*   If you want to display offline operators, we invite you to use the `connected=0` filter. Please note that you will only see agents that logged in to the iAdvize platform at least once.
*   If your operators have `skills` or `groups`, you need to specify it in your request.

#### Get operator's live availability
Get the live availability of an operator.

`GET /operator/123/live`

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    connected: false,
    chat: {
      enabled: false,
      slot_number: 1,
      slot_max_number: 2,
      busy: false,
      available: false
    },
    call: {
      enabled: true,
      slot_number: 1,
      slot_max_number: 1,
      busy: true,
      available: false
    },
    video: {
      enabled: false,
      slot_number: 0,
      slot_max_number: 1,
      busy: false,
      available: false
    }
  }
}
</pre>

#### Set operator's availability
Set the availability of an operator.

`PUT /operator/123/live`

**Fields**

| Field | Description | Value |
| --- | --- | --- |
| chat[available] | Set operator availability for chat channel | `1` (available) or `0` (unavailable) |
| call[available] | Set operator availability for call channel | `1` (available) or `0` (unavailable) |
| video[available] | Set operator availability for video channel | `1` (available) or `0` (unavailable) |
| connected | Set operator connection status | `0` (offline) - unique value possible |

**Response**

<pre class="prettyprint lang-js">{
  meta: {
    status: "success",
    message: "Operator is now available|unavailable for chat channel."
  }
}
</pre>

#### Get operators statistics

`GET /operator/123/statistic`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Operator identifier | Integer |
| conversation_number | Conversations number done by operator | Integer |
| ~~satisfaction_global_rate~~ (deprecated) | ~~Satisfaction average for operator conversations~~ | ~~Float~~ |
| experience | Operator experience | Integer |

**Response**

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    conversation_number: 589,
    satisfaction_global_rate: 0.86, // deprecated
    experience: 5630
  } 
}
</pre>

#### Get operator's profile

`GET /operator/123/profile`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| user_id | Operator identifier | Integer |
| status | Short text status written by operator | String |
| description | Operator profile description | String |
| facebook | Facebook identifier | String |
| twitter | Twitter identifier | String |
| city | City | String |
| country | Country | String |

**Response**

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    user_id: 123,
    status: "Je suis disponible pour vous aider",
    description: "Passionné par la menuiserie depuis plusieurs années, j'aime vous apporter des conseils.",
    facebook: "john.doe",
    twitter: "johndoe45",
    city: "Nantes",
    country: "France"
  }
}
</pre>

### Group

#### List your groups

`GET /group`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| parent_id | Parent group identifier | `?filters[parent_id]=1987` |

#### Get a group details

`GET /group/1984`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Group identifier | Integer |
| name | Group name | String |
| created_at | Date of creation | Date `YYYY-MM-DD HH:MM:SS` |
| parent_id | Parent identifier | Integer |
| operator_list | List of operators identifiers | List of integers |
| parent_list | List of parent's group ids | List of integers |

#### Create a group

`POST /group`

See [creating section](#create) to discover some output examples.

#### Update a group

`PUT /group/1`

See [updating section](#update) to discover some output examples.

#### Delete a group

`DELETE /group/1`

See [deleting section](#responses-delete) to discover some output examples.

### Skill

#### List your skills

`GET /skill`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| operator_id | Operator identifier | `?filters[operator_id]=123` |
| parent_id | Parent skill identifier | `?filters[parent_id]=123` |

#### Get a skill details

`GET /skill/1984`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Skill identifier | Integer |
| name | Name | String |
| order | Order | Integer |
| created_at | Date of creation | Date `YYYY-MM-DD HH:MM:SS` |
| parent_id | Parent skill identifier | Integer |
| operator_list **Deprecated: use the Operator resource with the skill_id filter instead** | List of operator identifiers | List of integers |

#### Create a skill

`POST /skill`

See [creating section](#create) to discover some output examples.

#### Update a skill

`PUT /skill/1`

See [updating section](#update) to discover some output examples.

#### Delete a skill

`DELETE /skill/1`

See [deleting section](#responses-delete) to discover some output examples.

### Conversation <span hidden>API</span>

#### List your conversations

`GET /conversation.json-unicode?formatHistory=0`

See below to discover used fields and see [reading section](#read) to discover some output examples.
Don't forget to use json-unicode path parameter & formatHistory query parameter to retrieve a well
formatted conversation history.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| channel | Channel | `chat`, `call`, `video` or `social` | `?filters[channel]=chat` |
| from | Date from (see more information below) | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[from]=2013-08-22` |
| to | Date to (see more information below) | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[to]=2013-08-25` |
| website_id | Website identifier | `?filters[website_id]=123` |
| operator_id | Operator identifier | `?filters[operator_id]=123` |
| visitor_id | Visitor identifier | `?filters[visitor_id]=123` |
| skill_id | Skill identifier | `?filters[skill_id]=123` |
| tag_id | Tag identifier | `?filters[tag_id]=123` |
| rule_id | Rule identifier | `?filters[rule_id]=123` |

A request cannot fetch the conversations for a period over 3 months.
The following rules apply :

*   If `from` and `to` are not specified, the last 3 months are fetched
*   If `from` is specified but not `to`, the 3 months after `from` are fetched
*   If `to` is specified but not `from`, the 3 months before `to` are fetched
*   If `from` and `to` are specified but with an interval over 3 months, an error is returned in the `meta` attribute of the response

#### Get a conversation details

`GET /conversation.json-unicode/666?formatHistory=0`

See [reading section](#read) to discover some output examples.
Don't forget to use json-unicode path parameter & formatHistory query parameter to retrieve a well
formatted conversation history.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Conversation identifier | Integer |
| channel | Conversation channel | `chat`, `call` or `video` |
| visitor_uid | Visitor unique identifier | String |
| history | Conversation history | String (see the different types of messages in the table below ‘Conversation history details‘) |
| operator_answer | Conversation answered by operator | Boolean |
| operator_closed | Conversation closed by operator | Boolean |
| waitinglist | Waiting list status | Boolean |
| page_type | Page type | String |
| created_at | Conversation start time | Date `YYYY-MM-DD HH:MM:SS` |
| closed_at | Conversation end time | Date `YYYY-MM-DD HH:MM:SS` |
| website_id | Website identifier | Integer |
| operator_id | Operator identifier | Integer |
| skill_id | Skill identifier | Integer |
| tag_list | List of tag identifiers | List of integers |
| rule_id | Rule identifier | Integer |
| xmpp_id | XMPP related identifier | UUID |


**Conversation history details**
You can retrieve different types of messages into the conversation.

| Field | Description | Values |
| :--- | :--- | :--- |
| history | Text message sent by Operator | `[1,"2016-02-16 11:24:43","Hello, how can I help you?",1455618283869]` |
| history | Text message sent by Visitor | `[2,"2016-02-16 11:25:26","I would like to know if my order: xxx has been sent",1455618327321]` |
| history | Software notifications | `[3,"2016-02-16 11:24:31","The chat rule has been activated."], [3,"2016-02-16 11:26:43","OPERATOR_CHAT_CLOSE"]` |
| history | URL - Link | `[5,"2016-02-16 11:24:21","http://iadvize.com/"]` |
| history | Rich content sent by Operator | `[6,"2016-02-16 11:24:21","http://img.png/"]` |
| history | Rich content sent by Visitor | `[7,"2016-02-16 11:24:21","http://img.png/"]` |

Conversation history types example
<pre class="prettyprint lang-js">
{
  [5,"2016-02-16 11:24:21","http://test.com/"],
  [2,"2016-02-16 11:24:23","Hello",1455618264049],
  [3,"2016-02-16 11:24:31","The chat rule has been activated."],
  [1,"2016-02-16 11:24:43","Hello, how can I help you?",1455618283869],
  [2,"2016-02-16 11:25:26","I would like to know if my order: xxx has been sent",1455618327321],
  [1,"2016-02-16 11:25:45","I check it, thank you for your patience",1455618346030],
  [1,"2016-02-16 11:26:02","Your order has been shipped",1455618363054],
  [2,"2016-02-16 11:26:09","Thanks, goodbye",1455618370072],
  [1,"2016-02-16 11:26:17","Goodbye",1455618377364],
  [3,"2016-02-16 11:26:43","OPERATOR_CHAT_CLOSE"]`
}
</pre>

### ~~Tag~~ deprecated

⚠️ **This resource is deprecated.** You should consider using our GraphQL API with the `conversationTag` object

#### List your tags

`GET /tag`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| website_id | Website identifier | `?filters[website_id]=123` |

#### Get a tag details

`GET /tag/123`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Tag identifier | Integer |
| name | Name | String |
| website_id | List of website identifiers | List of integers |

#### Create tags

`POST /tag`

**Parameters** (send an array of object as application/json)

| Field | Description | Values | Mandatory |
| --- | --- | --- | --- |
| name | Name | String | Yes |
| website_id | website identifier | Integer | Yes |

**Response**

<pre class="prettyprint lang-js">{
    meta: {
        status: "success"
    },
    data: [
        {
            id: 123,
            name: "my_value",
            website_id: 1,
            _link: "/tag/123"
        },
        {
            id: 124,
            name: "my_value_2",
            website_id: 1,
            _link: "/tag/124"
        }
    ]
}
</pre>

### Transaction

#### List your transactions

`GET /transaction`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| website_id | Website identifier | | `?filters[website_id]=123` |
| operator_id | Operator identifier | | `?filters[operator_id]=123` |
| conversation_id | Conversation identifier | Conversation identifier. You can also use `!null` & `null` to filter all transactions associated or not to a conversation. | `?filters[conversation_id]=123` `?filters[conversation_id]=null` `?filters[conversation_id]=!null` |
| from | Date from | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[from]=YYYY-MM-DD HH:MM:SS` |
| to | Date to | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[to]=YYYY-MM-DD HH:MM:SS` |

#### Get a transaction details

`GET /transaction/123`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Tag identifier | Integer |
| external_id | External identifier | String |
| visitor_uid | Visitor unique identifier | String |
| visitor_email | Visitor email | String |
| amount | Amount | Double |
| created_at | Date of creation | Date `YYYY-MM-DD HH:MM:SS` |
| website_id | Website identifier | Integer |
| operator_id | Operator identifier | Integer |
| conversation_id | Conversation identifier | Integer |

### ~~Satisfaction~~ deprecated

⚠️ **This resource is deprecated.** You should consider using our GraphQL API with the query `satisfactionSurveyResponses` or with the object `satisfactionSurvey` contained in the `searchClosedConversations` query.

#### List your satisfactions

`GET /satisfaction`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| website_id | Website identifier | `?filters[website_id]=123` | |
| operator_id | Operator identifier | `?filters[operator_id]=123` | |
| conversation_id | Conversation identifier | `?filters[conversation_id]=123` | |
| from | Date from | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[from]=YYYY-MM-DD HH:MM:SS` |
| to | Date to | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[to]=YYYY-MM-DD HH:MM:SS` |

#### Get a satisfaction details

`GET /satisfaction/123`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Satisfaction identifier | Integer |
| note_welcome | Welcome note | Double (percentage) |
| note_resolution | Resolution note | Double (percentage) |
| node_delay | Delay note | Double (percentage) |
| comment | Comment | String
| created_at | Date of creation | Date `YYYY-MM-DD HH:MM:SS` |
| website_id | Website identifier | Integer |
| operator_id | Operator identifier | Integer |
| conversation_id | Conversation identifier | Integer |

### Statistic

#### Get statistics

`GET /statistic`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| website_id `deprecated, use website_list property instead` | Website identifier | `?filters[website_id]=123` | |
| website_list | Website identifiers | `?filters[website_list]=123,24,32` | |
| channel | Channel | `chat`, `call`, `facebook`, `twitter`, `facebookBusinessOnMessenger`, `instagram`, `sms`, `whatsapp` or `video` | `?filters[channel]=chat` |
| resource | Resource to group the data by | `operator`, `group`, `skill`, `rule`, `contact_type` or `page_type` | `?filters[resource]=operator` |
| resource_id | Resource ID to get only the data of this resource | `?filters[resource_id]=32` | |
| indicators | Indicators to filter | See list below | `?filters[indicators]=indicator1,indicator2` |
| from | Date from | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[from]=YYYY-MM-DD` |
| to | Date to | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | `?filters[to]=YYYY-MM-DD` |
| granularity | Get data per hour, per day or per month (only when 1 indicator is requested) | `hour`, `day`, `month` | `?filters[indicators]=indicator1&filters[granularity]=day` |

#### Indicators

#### Contact indicators

**available on `chat`, `call`, `video`, `facebook`, `twitter`, `facebookBusinessOnMessenger`, `sms`, `whatsapp`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_answered_after_first_message_duration | Response time after first message | Average response time between a customer's first question and the agent's answer. | Second |
| contact_answered_duration | Response time | Average response time between a customer's request and the agent's response. | Second |
| contact_closed_after_last_message_duration | Length of time between last message and closing of chat | Average amount of time between the visitor's last message and the closing of the chat discussion on the panel. | Second |
| contact_duration | Average processing time | Average length of all contacts, the length of a contact being defined as the difference between the end time (closure) and start time. | Second |
| contact_number | Initiated contacts | Number of contacts initiated during the selected period. | Number |
| contact_sent_message_number | Sent messages | Total number of messages within a conversation sent by the agents. | Number |
| contact_received_message_number | Received messages | Total number of messages within a conversation received by the agents. | Number |
| contact_unanswered_number | Contacts initiated with no response | Number of contacts initiated by a visitor with no response from an agent. | Number |

**available on `chat`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_missed_number | Missed contact opportunities | Estimated number of missed contact opportunities because the agents were totally busy, offline or not in production. | Number |
| contact_missed_with_busy_operators_number | Missed contact opportunities (agents busy) | Estimated number of missed contact opportunities due to agents being totally busy. | Number |
| contact_missed_with_no_operators_number | Missed contact opportunities (agents absent) | Estimated number of contacts missed because the agents were either not connected or not in production. | Number |
| contact_simultaneous_number | Simultaneous contacts | Average number of contacts processed simultaneously by an agent during his online presence. | Number |

**available on `chat`, and `video`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_waiting_abort_number | Abandoned contacts | Number of contacts initiated in the queue who left before being processed. | Number |
| contact_waiting_answered_number | Processed contacts | Number of processed contacts coming from the queue.  | Number |
| contact_waiting_before_quit_duration | Waiting time before abandonment | Average time before a visitor abandons the queue. | Second |
| contact_waiting_duration | Waiting time before contact | Average waiting time of visitors in the queue. | Second |
| contact_waiting_number | Initiated contacts | Average waiting time of visitors in the queue. | Number |

**available on `chat`, `call`, `video`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_per_hour_average_number | Contacts / hr of the website | Average number of contacts processed by all agents for an hour of production. | Number |
| contact_per_hour_number | Contacts per hour | Average number of contacts processed by an agent for an hour of production. | Number |
| rule_contact_rate | Response rate | Proportion of displays having generated a contact. | Rate |
| rule_display_number | Displays | Number of chat/call displays generated on the website during the period. | Number |
| targeting_rule_triggered | Triggers | Number of times a targeting rule has been triggered, as a consequence of visitors meeting the right criteria. | Number |


#### Presence indicators

**available on `chat`, `call` and `video`**

| Indicator | Label | Description | Number |
| --- | --- | --- | --- |
| max_and_partial_occupation_duration | Global occupation | Period during which an agent is connected to the panel and is occupied partially or to the maximum. | Second |
| max_occupation_duration | Maximum occupation | Period during which an agent is connected to the panel and is occupied to maximum capacity. | Second |
| max_occupation_rate | Maximum occupation rate | Part of production time during which an agent is connected to the panel and is occupied to a maximum. | Rate |
| non_production_duration | Not in production | Period during which an agent is connected to the panel, unavailable and yet not busy. | Second |
| non_production_rate | Not in production rate | Proportion of connection time during which an agent is connected to the panel, unavailable and yet not busy. | Rate |
| presentation_duration | Smoothed period of button presentation | Period during which buttons are displayable. Length of the time slot covered with at least one agent available. | Second |
| production_smoothed_duration | Smoothed period of production | Period during which operators were in production. Length of the time slot covered with at least one agent in production. | Second |

**available on `chat`, `call`, `video`, `facebook`, `twitter` `facebookBusinessOnMessenger`, `sms`, `whatsapp`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| presence_duration | Total period of presence | Total period during which the agents were connected to the desk. |
| presence_smoothed_duration | Smoothed period of presence | Period during which operators were connected. Length of the time slot covered with at least one agent present. |
| occupation_rate | Partial occupation rate | Part of production time during which an agent is connected to the panel and is partially busy. |
| non_occupation_duration | Inocc. | Period of time during which an agent is connected to the panel and is simultaneously available and not busy. |
| non_occupation_rate | Rate of non-occupation | Part of production time during which an agent is connected to the panel and is simultaneously available and not busy. |
| max_and_partial_occupation_rate | Global occupation rate | Part of production time during which an agent is connected to the panel and is occupied partially or to the maximum. |
| production_duration | In production | Period during which an agent is connected to the panel and is available or busy. |


#### ~~Satisfaction indicators~~ deprecated

⚠️ **These indicators are no longer available in our REST API** since the new satisfaction is computed in a different way. You should consider using our GraphQL API with the query `satisfactionSurveyResponses` or with the object `satisfactionSurvey` contained in the `searchClosedConversations` query.

**available on `chat`, `call` and `video`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| satisfaction_delay_rate | Waiting time | Visitor satisfaction rate with the waiting time before receiving an answer. | Rate |
| satisfaction_global_rate | Overall satisfaction | Overall satisfaction rate of visitors. | Rate |
| satisfaction_resolution_rate | Quality of response | Visitors' satisfaction rate with the response given by the agent. | Rate |
| satisfaction_respondent_number | Number of respondents | Number of visitors who replied to a satisfaction survey following a discussion. | Number |
| satisfaction_respondent_rate | Response rate | Proportion of conversations after which visitors completed the satisfaction survey. | Rate |
| satisfaction_welcome_rate | Quality of welcome | Visitor satisfaction rate with the welcome. | Rate |
| occupation_duration | Partial occupation | Period during which an agent is connected to the panel, unavailable and yet not busy. | Second |


#### Transactions indicators

**available on `chat`, `call`, `video`, `facebook`, `twitter`, `facebookBusinessOnMessenger`, `sms`, `whatsapp`**

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| conversion_rate | Conversion rate | Proportion of conversations which led to transactions. | Rate |
| cart_after_contact_amount | Average order value after contact | Average order value following a contact. | Number |
| cart_global_amount | Average order value on the website | Average Order Value, all visitor categories. | Amount |
| transaction_after_contact_amount | T/O after contact | Total turnover from visitors who dialogued and completed a transaction after a contact. | Amount |
| transaction_after_contact_number | Transactions after contact |  Total number of transactions from visitors who dialogued and then completed a transaction following the contact. | Number |
| transaction_total_amount | Website T/O | Total turnover, all visitor categories. | Amount |
| transaction_total_number | Website transactions | Total number of transactions (all categories). | Number |
| transaction_after_contact_duration | Transformation time after contact | Average time between the first exchange and the transaction following a contact. | Second |
| transaction_after_conversation_amount_per_hour | Website transactions amount per hour | Average turnover generated by an agent after a contact on an hourly basis | Amount |
| transaction_missed_with_busy_operators_amount | T/O missed (agents totally busy) | Estimated lost turnover due to agents being totally busy. | Amount |
| transaction_missed_with_busy_operators_number | Missed transaction opportunities (agents totally busy) | Estimated number of missed transaction opportunities because the agents were totally busy. | Number |
| transaction_missed_with_no_operators_amount | Missed T/O opportunity (agents absent) | Estimated turnover missed because the agents were not connected or not in production. | Amount |
| transaction_missed_with_no_operators_number | Missed transaction opportunities (agents absent) | Estimated number of missed transaction opportunities because the agents were not connected or not in production. | Number |
| transaction_amount_per_conversation | Website transactions amount per conversation | Average turnover generated for each conversation done | Amount |


### Visitor

#### Get visitors

`GET /visitor`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| unique_id | Unique identifier | `?filters[unique_id]=123` |
| external_id | External identifier | `?filters[external_id]=123` |
| website_id | Website identifier | `?filters[website_id]=123` |

#### Get a visitor details

`GET /visitor/560`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Visitor identifier | Integer |
| unique_id | Visitor unique identifier | String |
| external_id | Your id if provided | String |
| lastname | Last name | String |
| firstname | First name | String |
| address | Address | String |
| city | City | String |
| zip | Zip code | String |
| country | Country | String |
| phone | Phone number | String |
| email | Email | String |
| browser | Browser used by visitor | String |
| website_id | List of website identifiers | List of integers |
| created_at | Visitor creation date | Date `YYYY-MM-DD HH:MM:SS` |

#### Create a visitor

`POST /visitor`

See [creating section](#create) to discover some output examples.

#### Update a visitor

`PUT /visitor/560`

See [updating section](#update) to discover some output examples.

#### Delete a visitor

`DELETE /visitor/560`

See [deleting section](#responses-delete) to discover some output examples.

### ~~Call meeting~~ deprecated

#### Get call meetings

`GET /callmeeting`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| website_id | Website identifier | `?filters[website_id]=123` |
| from | Period start date | `?filters[from]=2015-03-31 19:00:00` |
| to | Period end date | `?filters[to]=2015-06-31 18:00:00` |

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Call meeting identifier | Integer |
| phone_number | Visitor phone number | String |
| visitor_uid | Visitor unique identifier | String |
| status | Call meeting status (pending, progress, done, failed, working) | String |
| start_at | Date of call | DateTime |
| website_id | Website identifier | Integer |
| targeting_rule_id | Targeting rule identifier associated to call meeting | String |
| skill_id | Skill identifier associated to call meeting | String |

### ~~Callback Odigo~~ deprecated

#### Pick up callback

`POST /odigocallback/pickup`

**Parameters** (sent as application/x-www-form-urlencoded)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| operator_external_id | Operator external identifier | String | Yes |
| website_id | Website identifier | Integer | Yes |
| phone_number | Visitor phone number | String | Yes |

**Response**

<pre class="prettyprint lang-js">{
    meta: {
        status: "success"
    },
    data: {
        targeting_rule_id: 107,
        website_id: 1,
        conversation_id: 139,
        skill_id: null,
        visitor_phone_number: "0614037735",
        visitor_uid: "0a1572b7cc5027fe443f4203eaf0b98d4cbea6d313afa"
    }
}
</pre>

#### Hang up callback

`POST /odigocallback/hangup`
**Parameters** (sent as application/x-www-form-urlencoded)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| operator_external_id | Operator external identifier | String | Yes |
| website_id | Website identifier | Integer | Yes |
| phone_number | Visitor phone number | String | Yes |

**Response**

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: []
}
</pre>

