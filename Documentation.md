# General information
Welcome to iAdvize’s developer documentation!
If you want to use our API, create integrations for your own personal use or to share with the rest of the world, you are in the right place.

Early November 2017, iAdvize will provide you with a Developer platform for you to easily publish your apps on our marketplace so that our users can install them directly from their administration interface.

Whether you are a developer, an integrator, a customer or just curious, here, you will find an overview of how to get started, our Developer Guidelines, our API with practical examples and a guide to build and publish your future integrations.

## What is iAdvize?
[iAdvize](https://iadvize.com) is a conversational marketing platform that enables businesses to engage their customers and prospects whether they’re on the website or on social media from one single messaging solution (chat, voice, video). Visitors can get real-time advice from customer service but also from advocates, members of the brand community via [ibbü](https://www.ibbu.com/en/) - our on-demand pool of experts.

Implementing iAdvize is child's play. You just have to insert a tag on each page of your website. Once the solution is deployed, your customer service and marketing teams are completely independent and can set up the solution as they wish.

The iAdvize platform has 2 interfaces:

* The administration: administrators and managers of the solution can configure the platform's settings and monitor the agent's activity.

* The agent's console panel: it gives superpowers to your agents. That's the place where professional agents or experts can respond intuitively to all the messages they receive.

![iAdvize](./assets/images/%402XChatbox%20.jpg)
![iAdvize](./assets/images/%402XReports.jpg)

## What is the Developer Platform?

The iAdvize Developer Platform allows developers to build apps and use our public APIs.
Do you want to develop an app? We are providing you with documentation and a private testing environment.
(The Developer Platform will be available in private beta from November, 2017.)

## Why to build apps to iAdvize?

There are three main reasons for building an app with the iAdvize Developer Platform: 

* You build apps and publish them for our customer community. (We've got more than 500 customers to amaze!)
* You build apps in private mode and make them available only for one or more specific customers
* You get rewarded based on how frequently your apps are used

Here is the example of a potential protocol between iAdvize and a CRM software thanks to a connector:
![CRM Webhook](./assets/images/CRM-webhook.png)

# Getting Started
Do you want to join our developer community as a beta tester 🤘🏽? Follow these steps to be part of the adventure:

## Get a Developer Account
To build apps that iAdvize’s customers can use, first, you need to get a developer account.
The Developer Platform will be available in private beta version from November, 17. We invite you to apply to the early access program thanks to our [online form](https://docs.google.com/forms/d/e/1FAIpQLSfKbBBwHtXU60D0bw6dPejF1_h2VBiPAf60LpQWtJ7h6dvXeg/viewform?usp=sf_link).

* Apply and share your integration project with our team,
* The iAdvize team will contact you within 48 hours.

## Features Overview
iAdvize's Developer Platform will provide you with some easy-to-use tools so you can:

* Manager the privacy mode of your app for it to be public or private
* Set up the authentication process for your app
* Define custom settings such as object mapping (In progress)
* Create interactions to enhance some of iAdvize's predefined features
* Use outgoing webhooks to receive updates in real-time

Once your app is ready, you will be able to submit your connector for review.
Then, the iAdvize team will review your app to make sure it fits the Developer Platform policies, and will get back to you within 48 hours (on working days).
And then hurrah... You can publish your app on iAdvize’s marketplace!

# Build apps
Once you are logged in your developer account, you are ready to build apps.
So let's go through the different sections of the Developer Platform:

## My apps
This is the place where you can see the list of all the apps you have built on iAdvize. You can also see their current status:
* Published: your app is ready to be installed on the iAdvize Marketplace
* Under review: your app has been submitted for review
* Sandbox: you can edit your app

## App information
This is where you will be able to define your app's profile. Also, this is where you can set the Privacy mode of your application: public or private.

**How does the Private mode work?**
Your App can be available for all iAdvize's customers or for selected customers.
Our team is still working on the accessibility mode under the Private mode.
In alpha version, we will make it available manually for the specific customers you have selected.

## App Authentication
The App Authentication section is where you can set the authentication information that the final user will have to enter in order to install your connector. Once the user authenticated, the connector will be able to access the right data from iAdvize and from the third-party app. For example, you can ask the user for his/her third app's email and password.
Users will need to follow these authentication steps to install your app.

**Define app's authentication parameters**
You can add parameters and define the type of entry you need (text, numeric, etc.).

* Key: the key of your parameter according to your code.
* Label: it’s the name of your parameter, this is what users will see.
* Type: it defines the type of entry. (For instance: alphanumeric).

You can add as much parameters as you need.
This is the first thing users will see once they click on the "install" button on the iAdvize Marketplace.
Parameters appear to users according to their order of creation (the 1st entry created is the 1st on displayed on the page).

*i.e. if your primary goal is to know your users’ usernames, it is the first information you should ask them for.*

**Configure your verification url** 
On our side we will pre validate requirements of the parameters you have defined (mandatory, list values...).
Verification URL lets you implement your own installation validation logic.
For example you can check if API keys or username/password are valid on different systems. We will automatically call this URL if you fill in this 
Please find technical details in the [verification Url](#verification-url) section right below.

*i.e. users might be required to authenticate with an email and a password. In this case, you need to create two different parameters, one for the email and one for the password.*

![Authentication](./assets/images/developer-authentication.png)

Users have to fill in the parameters during the installation process first, on the iAdvize Marketplace.

![Authentication admin](./assets/images/marketplace-configure.png)

## App Settings

Just as in the section dedicated to your app's authentication, you are able to set the parameters that users will need to install your connector.
These are the parameters that the iAdvize administrator will fill in to install and configure your connector from the iAdvize Marketplace.

Define your app's settings parameters

You can add as many parameters as the installation and configuration of your application requires.
For each of these parameters you will have to specify the type of input required.

*Label: it is the name of your parameter. (This is what the users will see).
For instance it could be: Username
*Type: it defines the type of entry. (For instance: alphanumeric)
*ID: the identifier (key) of your parameter according to your code.

These configuration steps will take place immediately after authentication (if any).
The order of appearance of the steps depends on their order of creation. The first created parameter will appear first and the last created parameter will appear last to the user.

**Configure your verification url**
Like App authentication, you can define a verification URL tom implement your own logic on settings step.
For example you can check if some installation option compatibility with a custom logic of your connector.
Please find technical details in the [verification Url](#verification-url) section right below.

![Setting](./assets/images/developer-settings.jpg)

## Verification url

In the [app authentication](#app-authentication) and [app settings](#app-settings) sections of the iAdvize Developer Platform, you can set a "Verification url".
We will call this URL each time a client validate a step during an installation of your connector on a website.
the application requires a confirmation from your connector to approve the configuration settings.
It means that your connector must answer to this call by a confirmation or error messages to determine whether the step have been correctly set up. 
If the step is validated by your connector, parameters are saved on our side.

### Request payload

Here is the information sent to your verification url as a payload body of a POST Request.

<pre class="prettyprint lang-js">
[
    {
		"key": "login",
		"value": "login"
	},
	{
		"key": "password",
		"value": "p4ssw0rd"
	}
]
</pre>

| Field | Description | Values |
| --- | --- | --- |
| key | Parameter key, defined by you in developer platform | String |
| value | Parameter value, filled by the client during connector's installation | String|Boolean  |


### Response payload 

In order to validate the information filled by the iAdvize administrator during the installation of the connector, we await the answer of your connector in this format:

<pre class="prettyprint lang-js">
{
	"isStepValid": false,
	"errors": [
	    {
            "code": "password",
            "description": "password is not valid",
            "parameterKey": "login"
        }
	]
}
</pre>

| Field | Description | Values | Required |
| --- | --- | --- | --- |
| isValid | validation status | Boolean | ✓ |
| errors | Errors list, can be empty | Array | ✓ |
| errors - code| Error code, used to identify error on connector side | String | ✓ |
| errors - message | Error message that will be displayed on our installation process | String | ✓ |
| errors - parameterKey | If mentioned, error concerns this parameter key | String | ✓ |

## App Interactions
Use interactions to enhance the iAdvize interface by adding or editing predefined features. 

Interactions are basically HTTP endpoints whose json responses fit the interaction json-schema. For each interaction one or more endpoint have to be defined. When interaction is used on user interface, we will make a GET http call to endpoint with documented query parameters. Your http response have to comply with interaction json-schema.

The features that are already available are: 

* The product List (on the discussion panel)
* The visitor profile (on the discussion panel)
* The conversation closing form (on the discussion panel)

### The product list
The integration of the product list enables iAdvize's Console panel users to browse a product catalog from the iAdvize discussion panel.
Agents can look for a product while they are chatting and send it in just a click within their conversation.

Products are displayed in a popup window just over the conversations view: When shared, visitors can see their image, title, availability and price.
By clicking on the "view product" button, visitors are redirected to the product page on your website.

![Product list](./assets/images/interactions-product-list-feature.png)

**Add the product list interaction and configure it**

To make sure your connector uses the Product list interaction correctly, all you have to do is to declare:
* The product list URL - this is your catalog’s URL
* The categories url - this is where your connector will get the list of your product categories

#### Categories data

<pre class="prettyprint lang-js">
[
    {
        "id": "123",
        "idParent": "123",
        "label": "category",
        "products": [
            "123",
            "456"
        ],
        "productsCount": 3
     },
     {
         "id": "456",
         "idParent": null,
         "label": "category",
         "products": null,
         "productsCount": 7
      }
 ]
</pre>


** Request - GET method **

| Query parameter | Description | Values |
| --- | --- | --- |
| idConnectorVersion | Connector version id | ?idConnectorVersion=123 |
| idParent | Unique identifier of the parent category | ?idParent=123  |
| idWebsite | Unique identifier of the associated website (assigned to you by iAdvize) | ?idWebsite=123  |
| idOperator | Unique identifier of the operator loading the categories | ?idOperator=9999  |
| limit | Maximum number of resources per page | ?limit=10 |
| offset | Number of resources skipped before beginning to return resources | ?offset=10 |

** Response - Array of categories **

| Field | Description | Values | Required |
| --- | --- | --- | --- |
| id | Unique identifier | Integer | ✓ |
| idParent | Unique identifier of the parent category  | Integer |  |
| label | Label | String | ✓ |
| products | products | Array of strings |  |
| productsCount | Number of products | Integer | ✓ |

#### Products data

<pre class="prettyprint lang-js">
[
    {
        "id": "123",
        "title": "Product's title",
        "productUrl": "http://www.e-commerce.com/url-product",
        "brand": "brand",
        "description": "product's description",
        "shortDescription": "shrot description",
        "available": true,
        "imageUrl": "http://www.e-commerce.com/url-product-image.jpg",
        "reference": "reference",
        "priceCatalog": "99.9 €",
        "pricePromotion": "90 €",
        "priceSpecial": "80 €"
    },
    {
        "id": "456",
        "title": "Product's title",
        "productUrl": "http://www.e-commerce.com/url-product",
        "brand": null,
        "description": "product's description",
        "shortDescription": null,
        "available": true,
        "imageUrl": "http://www.e-commerce.com/url-product-image.jpg",
        "reference": null,
        "priceCatalog": "9.9 €",
        "pricePromotion": null,
        "priceSpecial": null
    }
]
</pre>


** Request - GET method **

| Query parameter | Description | Values |
| --- | --- | --- |
| idConnectorVersion | Connector version id | ?idConnectorVersion=123 |
| idCategory | Category id | ?idCategory=123  |
| idWebsite | Unique identifier of the associated website (assigned to you by iAdvize) | ?idWebsite=123  |
| idOperator | Unique identifier of the operator loading the products | ?idOperator=9999  |
| limit | Maximum number of resources per page | ?limit=10 |
| offset | Number of resources skipped before beginning to return resources | ?offset=10 |
| searchQuery | Product search query | ?searchQuery=query |

** Response - Array of products **

| Field | Description | Values | Required |
| --- | --- | --- | --- |
| id | Unique identifier | Integer | ✓ |
| title | Title | String | ✓ |
| productUrl | Product's url | String | ✓ |
| brand | Brand | String |  |
| description | Description | String | ✓ |
| shortDescription | Short description | String |  |
| available | Availability | Boolean |  |
| imageUrl | Image's url | String | ✓ |
| reference | Reference | String | ✓ |
| priceCatalog | Price catalog | String | ✓ |
| pricePromotion | Price promotion | String |  |
| priceSpecial | Price special | String |  |

### The visitor profile

The visitor profile interaction enables iAdvize's Console panel users to access to the visitor's CRM profile in a single click. 
Agents can overview the visitor's CRM profile in a new window while they are chatting. Operators can then edit it or simply look for information.

To be able to retrieve the CRM profile, iAdvize must be able to identify the visitor thanks to an email and/or an external ID.

![VisitorProfile](./assets/images/visitorprofilefeature@2x.png)

**Add a visitor profile connector and configure it**
In order to set the right connector parameters, all you have to do is to declare:
* The connector URL - this is your visitor's profile URL

#### Visitor profile data

<pre class="prettyprint lang-js">
 [
    {
        "id":"1",
        "label": "CRM profile",
        "value": "https://www.crm.fr/visitor-profile",
        "fieldType":"URL"
    },
    {
        "id":"2",
        "label": "CRM tag",
        "value": "tag",
        "fieldType": "TEXT"
    }
 ]
</pre>


** Request - GET method **

| Query parameter | Description | Values |
| --- | --- | --- |
| emailVisitor | Visitor email | ?emailVisitor=123  |
| idConnectorVersion | Connector version id | ?idConnectorVersion=123 |
| idVisitorExternal | Visitor external id | ?idVisitorExternal=123  |
| idVisitorUnique | Visitor unique id | ?idVisitorUnique=123  |
| idWebsite | Unique identifier of the associated website (assigned to you by iAdvize) | ?idWebsite=123  |
| operatorLocale | Operator locale | ?operatorLocale=en  |
| idOperator | Unique identifier of the operator loading the visitor profile | ?idOperator=9999  |

** Response - Array of fields **

| Field | Description | Values | Required |
| --- | --- | --- | --- |
| id | Unique identifier | Integer | ✓ |
| label | Label | String | ✓ |
| value | Value | String | ✓ |
| fieldType | Field type | `URL` or `TEXT` | ✓ |

### The conversation closing form

The conversation closing form interaction enables iAdvize's Console panel users to provide additional information manually at the end of conversation. 

![CloseConversation](./assets/images/close_conversation@2x.png)

**Add a conversation closing form connector and Configure it**
In order to set the right connector parameters, all you have to do is to declare:
* The connector URL - this is your form's url

#### Conversation Closing Form data

<pre class="prettyprint lang-js">
 [
    {
        "id": "1",
        "label": "create a salesforce ticket",
        "fieldType": "CHECKBOX",
        "isRequired": true
    },
    {
        "id": "2",
        "idParent": "1",
        "label": "Brand name",
        "fieldType": "TEXT",
        "isRequired": true
    },
    {
        "id": "3",
        "idParent": "1",
        "label": "Color",
        "fieldType": "TEXT",
        "isRequired": true
    }
]
</pre>


** Request - GET method **

| Query parameter | Description | Values |
| --- | --- | --- |
| idConnectorVersion | Connector version id | ?idConnectorVersion=123 |
| idWebsite | Unique identifier of the associated website (assigned to you by iAdvize) | ?idWebsite=123  |
| operatorLocale | Operator locale | ?operatorLocale=en  |
| idOperator | Unique identifier of the operator loading the form | ?idOperator=9999  |

** Response - Array of inputs **

| Field | Description | Values | Required |
| --- | --- | --- | --- |
| id | Unique identifier | string | ✓ |
| idParent | Parent identifier, if the field depends on it| string | |
| label | Label | String | ✓ |
| fieldType | Field type | `TEXT` or `CHECKBOX` | ✓ |
| isRequired | Required | Boolean | ✓ |

## Submit your apps

Apps must be submitted to iAdvize for review.
The versioning declaration must be done by the developer during the submission process.
iAdvize will approve or refuse the app based on specific criteria.
iAdvize will get in touch within 48 hours to the developers.

## App security

For security reasons iAdvize provides you with a method to verify and secure your apps. You will be able to make sure that the payloads have not been subjected to modifications, and to verify its source in order for example to limit the requests to those coming from iAdvize.

Once your server is configured to receive payloads, you can set up a secret token and verify the information.

### Set you secret token

First, you need to get one secret token depending on your connector.
You can retrieve this token in the 'App information' section on our developer platform.

### Validating payloads from iAdvize

Once the secret token set, iAdvize will create a hash signature. 
This hash signature is passed along with each request in the headers as `X-iAdvize-Signature`. 
Hash signature starts with algorithm name `sha256=` and is computed by hashing query string with HMAC hexdigest algorithm and your secret token as salt. 

<pre class="prettyprint lang-js">
X-iAdvize-Signature: sha256=110e8400-e29b-11d4-a716-446655440000
</pre>


You have to compute a new hash using your secret token, and to compare it with `X-iAdvize-Signature` and make sure it matches.

<pre class="prettyprint lang-php">
$secretToken       = 'yourSecretToken';
$queryString       = $request->getUri()->getQuery();
$iAdvizeSignature  = $headers['X-iAdvize-Signature'];

// Get alogrithm and hash
list($algorithm, $iAdvizeHash) = explode('=', $iAdvizeSignature, 2);
 
// Computed hash with query parameters
$queryParametersHash = hash_hmac($algorithm, $queryString, $secretToken);
 
// Final check
if (! hash_equals($iAdvizeHash, $queryParametersHash)) {
    exit('Validation hash failed');
}
</pre>


We strongly recommend you, to use the **constant time** string comparison method (`hash_equals` vs `===`  in our example), 
to be less vulnerable to [timing attacks](https://en.wikipedia.org/wiki/Timing_attack).

## Add webhooks
The webhook system allows external applications to subscribe to events (via callback URLs) to receive updates in real-time.
When you build your app, you can subscribe to a list of events.
When customers install your app, it automatically creates webhooks for these customers as well as for events based on your app's configuration.

This subscription is based on the events happening on different domains. See the list of events available in the [Webhooks documentation](#webhooks).

You can create as much outgoing webhooks as you need.
A webhook can cover several events.
An event can be linked to a customer (example customers.website.created)
or linked to a website (example customers.website.created)

* Name of the webhook: an optional label you can give to the webhook
* webhook URL: the server URL that will receive the webhook
* Security token: Token provided by iAdvize (this field cannot be edited)
* Content-type: Application / json ; Application / x-www-form-urlencoded
* Events: you can select the events in the list. You can subscribe to all
iAdvize events, all events of a specific domain, or only one event.


## Developer Policy
Developers host their code on their own host service.
Developers are responsible for their connector's maintenance.
Developers can set their app’s price (monthly fee per user).
If it’s not a free app, developers must be a legal person.

# REST API
**Current version:** 2.0

This API provides access and basic CRUD operations (create, read, update, delete) for the resources described in the documentation.
The REST API uses JSON exclusively. XML is not supported.

## Base URL

All URLs referenced in the documentation have the following base:

| Standard platform | High availability platform |
| --- | --- |
| `https://www.iadvize.com/api/2` | `https://ha.iadvize.com/api/2` |

The iAdvize REST API is served over HTTPS and HTTP.

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

##### `POST /my_resource my_field=my_value (with error)`

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
| page | Page number | ?page=1 |
| limit | Maximum number of resources per page (maximum possible value is 100) | ?limit=1 |
| full | Show all fields of the resource | ?full=1 |

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

**DELETE /my_resource/456 (with error)**

<pre class="prettyprint lang-js">{
  meta: {
    status: "fail"
    message: "Unknown 'my_resource' with 'id' 456"
  }
}
</pre>

## Resources

### Client

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

### Website

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


#### Update a website

`PUT /website/1`

See [updating section](#update) to discover some output examples.

### Operator

#### List your operators

`GET /operator`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- |
| id | Operator identifier | | ?filters[id]=123 |
| group_id | Group identifier | | ?filters[group_id]=123 |
| website_id | Website identifier | | ?filters[website_id]=123 |
| skill_id | Skill identifier | | ?filters[skill_id]=123 |
| name | Operator name | | ?filters[name]=genius |
| external_id | External identifier | | ?filters[external_id]=MyExternalId |
| connected | Operator online status | 0 (offline) or 1 (online) | ?filters[connected]=1 |

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
| sso_key | [SSO token](/?p=sso) | String |

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
*   If you want to display offline operators, we invite you to use the `connected` filter. Please note that you will only see agents that logged in to the iAdvize platform at least once.
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
| satisfaction_global_rate | Satisfaction average for operator conversations | Float |
| experience | Operator experience | Integer |

**Response**

<pre class="prettyprint lang-js">{
  meta: {
    status: "success"
  },
  data: {
    id: 123,
    conversation_number: 589,
    satisfaction_global_rate: 0.86,
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

##### Response

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
| parent_id | Parent group identifier | ?filters[parent_id]=1987 |

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
| operator_id | Operator identifier | ?filters[operator_id]=123 |
| parent_id | Parent skill identifier | ?filters[parent_id]=123 |

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
| operator_list`deprecated, use the Operator resource with the skill_id filter instead` | List of operator identifiers | List of integers |

#### Create a skill

`POST /skill`

See [creating section](#create) to discover some output examples.

#### Update a skill

`PUT /skill/1`

See [updating section](#update) to discover some output examples.

#### Delete a skill

`DELETE /skill/1`

See [deleting section](#responses-delete) to discover some output examples.

### Conversation

#### List your conversations

`GET /conversation`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| channel | Channel | `chat`, `call`, `video` or `social` | ?filters[channel]=chat |
| from | Date from (see more information below) | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | ?filters[from]=2013-08-22 |
| to | Date to (see more information below) | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | ?filters[to]=2013-08-25 |
| website_id | Website identifier | ?filters[website_id]=123 |
| operator_id | Operator identifier | ?filters[operator_id]=123 |
| visitor_id | Visitor identifier | ?filters[visitor_id]=123 |
| skill_id | Skill identifier | ?filters[skill_id]=123 |
| tag_id | Tag identifier | ?filters[tag_id]=123 |
| rule_id | Rule identifier | ?filters[rule_id]=123 |

A request cannot fetch the conversations for a period over 3 months.
The following rules apply :

*   If `from` and `to` are not specified, the last 3 months are fetched
*   If `from` is specified but not `to`, the 3 months after `from` are fetched
*   If `to` is specified but not `from`, the 3 months before `to` are fetched
*   If `from` and `to` are specified but with an interval over 3 months, an error is returned in the `meta` attribute of the response

#### Get a conversation details

`GET /conversation/666`

See [reading section](#read) to discover some output examples.

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
| history | Text message sent by Operator | [1,"2016-02-16 11:24:43","Hello, how can I help you?",1455618283869], |
| history | Text message sent by Visitor | [2,"2016-02-16 11:25:26","I would like to know if my order: xxx has been sent",1455618327321], |
| history | Software notifications | [3,"2016-02-16 11:24:31","The chat rule has been activated."], [3,"2016-02-16 11:26:43","OPERATOR_CHAT_CLOSE"] |
| history | URL - Link | [5,"2016-02-16 11:24:21","http://iadvize.com/"] |
| history | Rich content sent by Operator | [6,"2016-02-16 11:24:21","http://img.png/"] |
| history | Rich content sent by Visitor | [7,"2016-02-16 11:24:21","http://img.png/"] |

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

### Tag

#### List your tags

`GET /tag`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Use |
| --- | --- | --- |
| website_id | Website identifier | ?filters[website_id]=123 |

#### Get a tag details

`GET /tag/123`

See [reading section](#read) to discover some output examples.

**Fields**

| Field | Description | Values |
| --- | --- | --- |
| id | Tag identifier | Integer |
| name | Name | String |
| website_id | List of website identifiers | List of integers |

#### Create tag(s)

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

### Satisfaction

#### List your satisfactions

`GET /satisfaction`

See below to discover used fields and see [reading section](#read) to discover some output examples.

**Filters**

| Filter | Description | Values | Use |
| --- | --- | --- | --- |
| website_id | Website identifier | ?filters[website_id]=123 | |
| operator_id | Operator identifier | ?filters[operator_id]=123 | |
| conversation_id | Conversation identifier | ?filters[conversation_id]=123 | |
| from | Date from | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | ?filters[from]=YYYY-MM-DD HH:MM:SS |
| to | Date to | `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS` | ?filters[to]=YYYY-MM-DD HH:MM:SS |

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

##### available on `chat`, `call`, `video`, `facebook`, `twitter`, `facebookBusinessOnMessenger`, `sms`, `whatsapp`

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

##### available on `chat`

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_missed_number | Missed contact opportunities | Estimated number of missed contact opportunities because the agents were totally busy, offline or not in production. | Number |
| contact_missed_with_busy_operators_number | Missed contact opportunities (agents busy) | Estimated number of missed contact opportunities due to agents being totally busy. | Number |
| contact_missed_with_no_operators_number | Missed contact opportunities (agents absent) | Estimated number of contacts missed because the agents were either not connected or not in production. | Number |
| contact_simultaneous_number | Simultaneous contacts | Average number of contacts processed simultaneously by an agent during his online presence. | Number |

##### available on `chat`, and `video`

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_waiting_abort_number | Abandoned contacts | Number of contacts initiated in the queue who left before being processed. | Number |
| contact_waiting_answered_number | Processed contacts | Number of processed contacts coming from the queue.  | Number |
| contact_waiting_before_quit_duration | Waiting time before abandonment | Average time before a visitor abandons the queue. | Second |
| contact_waiting_duration | Waiting time before contact | Average waiting time of visitors in the queue. | Second |
| contact_waiting_number | Initiated contacts | Average waiting time of visitors in the queue. | Number |

##### available on `chat`, `call`, `video`

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| contact_per_hour_average_number | Contacts / hr of the website | Average number of contacts processed by all agents for an hour of production. | Number |
| contact_per_hour_number | Contacts per hour | Average number of contacts processed by an agent for an hour of production. | Number |
| rule_contact_rate | Response rate | Proportion of displays having generated a contact. | Rate |
| rule_display_number | Displays | Number of chat/call displays generated on the website during the period. | Number |
| targeting_rule_triggered | Triggers | Number of times a targeting rule has been triggered, as a consequence of visitors meeting the right criteria. | Number |


#### Presence indicators

##### available on `chat`, `call` and `video`

| Indicator | Label | Description | Number |
| --- | --- | --- | --- |
| max_and_partial_occupation_duration | Global occupation | Period during which an agent is connected to the panel and is occupied partially or to the maximum. | Second |
| max_occupation_duration | Maximum occupation | Period during which an agent is connected to the panel and is occupied to maximum capacity. | Second |
| max_occupation_rate | Maximum occupation rate | Part of production time during which an agent is connected to the panel and is occupied to a maximum. | Rate |
| non_production_duration | Not in production | Period during which an agent is connected to the panel, unavailable and yet not busy. | Second |
| non_production_rate | Not in production rate | Proportion of connection time during which an agent is connected to the panel, unavailable and yet not busy. | Rate |
| presentation_duration | Smoothed period of button presentation | Period during which buttons are displayable. Length of the time slot covered with at least one agent available. | Second |
| production_smoothed_duration | Smoothed period of production | Period during which operators were in production. Length of the time slot covered with at least one agent in production. | Second |

##### available on `chat`, `call`, `video`, `facebook`, `twitter` `facebookBusinessOnMessenger`, `sms`, `whatsapp`

| Indicator | Label | Description | Value |
| --- | --- | --- | --- |
| presence_duration | Total period of presence | Total period during which the agents were connected to the desk. |
| presence_smoothed_duration | Smoothed period of presence | Period during which operators were connected. Length of the time slot covered with at least one agent present. |
| occupation_rate | Partial occupation rate | Part of production time during which an agent is connected to the panel and is partially busy. |
| non_occupation_duration | Inocc. | Period of time during which an agent is connected to the panel and is simultaneously available and not busy. |
| non_occupation_rate | Rate of non-occupation | Part of production time during which an agent is connected to the panel and is simultaneously available and not busy. |
| max_and_partial_occupation_rate | Global occupation rate | Part of production time during which an agent is connected to the panel and is occupied partially or to the maximum. |
| production_duration | In production | Period during which an agent is connected to the panel and is available or busy. |


#### Satisfaction indicators

##### available on `chat`, `call` and `video`

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

##### available on `chat`, `call`, `video`, `facebook`, `twitter`, `facebookBusinessOnMessenger`, `sms`, `whatsapp`

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

### Call meeting

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

### Callback Odigo

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


# GraphQL API <span class="tag">alpha</span>

## Getting started on GraphQL

GraphQL is our new API, all new resources will only be exposed in this new API.
We are currently migrating old resources from Rest API to GraphQL.
Please note that we are in alpha version, resources are pretty stable but
authentication method will change in the next months.

One of the power of GraphQL API is to allow you retrieve many resources in one HTTP call.
You can request only fields you need. If you wan to learn more about GraphQL, please check [Learn GraphQL](https://graphql.org/learn/)

## Authentication <span hidden>on GraphQL</span>

Authentication uses temporary & revocable access tokens.
You can generate an access token by calling the url below with a user email & password.

`POST /oauth2/token`
**Parameters** (sent as application/x-www-form-urlencoded)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| username | User email | String | Yes |
| password | User password | String | Yes |
| grant_type | Oauth2 grant type (only password is supported) | String | Yes |

<pre class="prettyprint lang-js">
{
    "refresh_token": "***************************",
    "token_type": "bearer",
    "expires_in": 86400,
    "access_token": "***************************"
}
</pre>

<pre class="prettyprint lang-bash">
    curl -XPOST https://api.iadvize.com/oauth2/token -d "username={EMAIL}&password={PASSWORD}&grant_type=password"
</pre>

To authenticate an API call just pass the access token in an authorization header.
You can verify token validity with the authenticated route below.

<pre class="prettyprint lang-bash">
    curl -H "Authorization: Bearer {ACCESS_TOKEN}" https://api.iadvize.com/_authenticated
</pre>

## Resources <span hidden>GraphQL</span>

[Documentation GraphQL](/bundles/devplatformapp/graphqldoc/index.html)

## Example

To use the GraphQL API, call the URL below with the Authorization header containing your access token.

`POST /graphql`
**Parameters** (sent as application/json)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| query | GraphQL query | String | Yes |
| variables | Variables to be used in the GraphQL query | String | No |
| operationName | Operation to perform if the GraphQL query contains several operations | String | No |

###For example:
<pre class="prettyprint lang-js">{
  "query": "query GetConnector($connectorId: UUID!) { connector(id: $connectorId) { name } }",
  "variables": {
    "connectorId": "41c64064-4729-4d83-a939-8d46ac06d207"
  }
}
</pre>

###Result:
<pre class="prettyprint lang-js">{
  "data": {
    "connector": {
      "name": "..."
    }
  }
}
</pre>

# Webhooks

## Events description

| Domain | Name | Description |
| --- | --- | --- |
| conversations.domain | `conversation.started` | Chat or call conversation |
| conversations.domain | `conversation.closed` | Chat or call conversation |
| conversations.domain | `conversation.transferred` | Chat conversation |
| conversations.domain | `visitor.updated` | Visitor information updated from desk or admin view |
| users.domain | `user.created` | User created |
| users.domain | `user.updated` | User information updated |
| users.domain | `satisfaction.filled` | |
| users.domain | `user.connected` | |
| users.domain | `user.disconnected` | |


## Payloads
When an event occurs, an HTTP POST call is issued on the callback urls you set up with the event data. 
Data is sent with “application/json” header content-type, and “json” format as payload. 
Callback urls must be defined with HTTPS protocol and should be available with POST verb to send data payload.
iAdvize expect to have à 20x http status in callback result.

**Output examples of Conversations domain:**

Please note : 

| Attribut | Description |
| --- | --- |
| clientId | As a client of iAdvize you have a specific ID, it is what this one represents |
| visitorId | Each visitor has a unique ID. iAdvize calls it visitor unique ID |

#### conversation.started

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

#### conversation.closed

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

#### conversation.transferred

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

#### satisfaction.filled
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

#### connector.installed
<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "connector.installed",
    "platform": "SD",
    "websiteId": 1,
    "connectorId": "3f0e6840-48fe-4e87-8f3b-6ef3f75f18d8",
    "connectorVersionId": "3f0e6840-48fe-4e87-8f3b-6ef3f75f18d8",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
}
</pre>

#### connector.uninstalled
<pre class="prettyprint lang-js">{
    "eventId": "d36cd3c4-2d16-4a77-97c2-620bde859b29",
    "eventType": "connector.uninstalled",
    "platform": "SD",
    "websiteId": 1,
    "connectorId": "3f0e6840-48fe-4e87-8f3b-6ef3f75f18d8",
    "connectorVersionId": "3f0e6840-48fe-4e87-8f3b-6ef3f75f18d8",
    "createdAt": "2017-04-22T11:01:00+02:00",
    "sentAt": "2017-04-22T11:01:00+02:00"
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

For security reasons iAdvize provides you with a method to verify and secure your Webhooks notifications. You will be able to make sure that the payloads have not been subjected to modifications, and to verify its source in order for example to limit the requests to those coming from iAdvize.

Once your server is configured to receive payloads, you can set up a secret token and verify the information.

### Set you secret token

First, you need to get one or several secret token depending on your project.

If you build a connector thanks to our Developer Platform, you will have to use one token per connector (no matters the number of webhook you set within your connector).
You can retrieve this token in the 'App information' section.

If you want to use the webhook system without building a connector, you will have to use one token per webhook.
To retrieve the token(s) you must contact us at developers@iadvize.com and we will generate the token for you.

### Validating payloads from iAdvize

Once the secret token set, iAdvize will create a hash signature. 
This hash signature is passed along with each request in the headers as `X-iAdvize-Signature`. 
Hash signature starts with algorithm name `sha256=` and is computed by hashing body payload with HMAC hexdigest algorithm and your secret token as salt. 

<pre class="prettyprint lang-js">
X-iAdvize-Signature: sha256=110e8400-e29b-11d4-a716-446655440000
</pre>


You have to compute a new hash using your secret token, and to compare it with `X-iAdvize-Signature` and make sure it matches.
Here is an example of a PHP implementation:

<pre class="prettyprint lang-php">
$secretToken       = 'yourSecretToken';
$headers           = getallheaders();
$iAdvizeSignature  = $headers['X-iAdvize-Signature'];

// Get alogrithm and hash
list($algorithm, $iAdvizeHash) = explode('=', $iAdvizeSignature, 2);
 
// Get body payload from webhook
$bodyPayload = file_get_contents('php://input');
 
// Computed hash with body payload
$bodyPayloadHash = hash_hmac($algorithm, $bodyPayload, $secretToken);
 
// Final check
if (! hash_equals($iAdvizeHash, $bodyPayloadHash)) {
    exit('Validation hash failed');
}
</pre>


We strongly recommend you, to use the **constant time** string comparison method (`hash_equals` vs `===`  in our example), 
to be less vulnerable to timing attacks.

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

# Single Sign On

iAdvize offers a [Single Sign On](http://en.wikipedia.org/wiki/Single_sign-on) method that allows you to provide a unique authentication system to your operators who are already logged to your app.

## Benefits

If your users have to switch between several apps (including iAdvize) during their daily work, Single Sign On method has some interesting benefits :

*   Reducing password fatigue from different user name and password combinations
*   Reducing time spent re-entering passwords for the same identity
*   Reducing IT costs due to lower number of IT help desk calls about passwords

## Implementation

To connect an operator to its iAdvize console :

*   Get his sso_key in the [operator resource of the REST API](#operator).
*   Use it in the following URL : `https://www.iadvize.com/admin/login?key={SSO_KEY}`

That's all! When a user visit the URL, he will be automatically logged to its iAdvize account and no login / password will be asked to him.

## Use specific links

It's possible to use a specific link with a parameter called `dest` to go to a specific page.

Examples below:

| Page | URL |
| --- | --- |
| Discussion panel | `https://www.iadvize.com/admin/login?key={SSO_KEY}&dest=/pupitre` |
| Users | `https://www.iadvize.com/admin/login?key={SSO_KEY}&dest=/admin/users` |

To find the parameter `dest` that interest you, look the URL address of the page in your favorite web browser.

![URL example](./assets/images/sso-url.png)

With this example, the SSO URL address will be:
`https://www.iadvize.com/admin/login?key={SSO_KEY}&dest=/admin/users/`
