# GraphQL API

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
