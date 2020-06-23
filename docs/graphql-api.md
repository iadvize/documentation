# GraphQL API

## Getting started on GraphQL

GraphQL is our new API, all new resources will only be exposed in this new API.
We are currently migrating old resources from Rest API to GraphQL.
Please note that we are in alpha version, resources are pretty stable but
authentication method will change in the next months.

One of the power of GraphQL API is to allow you retrieve many resources in one HTTP call.
You can request only fields you need. If you wan to learn more about GraphQL, please check [Learn GraphQL](https://graphql.org/learn/).

A lot of GraphQL clients are available in [Official GraphQL documentation](https://graphql.org/code/#graphql-clients).

## Authentication <span hidden>on GraphQL</span>

Authentication uses temporary & revocable access tokens.

⚠️ Please note that the token lifetime is 24 hours

You can generate an access token by calling the url below with a user email & password.

`POST https://api.iadvize.com/oauth2/token`
**Parameters** (sent as application/x-www-form-urlencoded)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| username | User email | String | Yes |
| password | User password | String | Yes |
| grant_type | Oauth2 grant type (only password is supported) | String | Yes |

<pre class="prettyprint lang-sh">
curl --request POST \
     --url 'https://api.iadvize.com/oauth2/token' \
     --data 'username={EMAIL}&password={PASSWORD}&grant_type=password'
</pre>

<pre class="prettyprint lang-js">
{
    "refresh_token": "***************************",
    "token_type": "bearer",
    "expires_in": 86400,
    "access_token": "***************************"
}
</pre>

To authenticate an API call just pass the access token in an authorization header.
You can verify token validity with the authenticated route below.

<pre class="prettyprint lang-sh">
curl --request GET \
     --url https://api.iadvize.com/_authenticated \
     --header 'Authorization: Bearer {ACCESS_TOKEN}'
</pre>

## Documentation and tooling

[Documentation GraphQL](/bundles/devplatformapp/graphqldoc/index.html)

See static documentation of our GraphQL types, queries and mutation.

[Test our GraphQL API](/tools/graphiql)

Get your API key and make requests to our GraphQL API with ease.

[Explore our GraphQL API](/tools/voyager-view)

Display graphically all our Graph, ressources and links between them.

## Examples <span hidden>GraphQL</span>

To use the GraphQL API, call the URL below with the Authorization header containing your access token.

`POST /graphql`

**Parameters** (sent as application/json)

| Parameter | Description | Values | Mandatory |
| --- | --- | --- | --- |
| query | GraphQL query | String | Yes |
| variables | Variables to be used in the GraphQL query | String | No |
| operationName | Operation to perform if the GraphQL query contains several operations | String | No |

**Complete example**

<pre class="prettyprint lang-sh">
curl --request POST \
     --url 'https://api.iadvize.com/graphql' \
     --header 'authorization: Bearer {ACCESS_TOKEN}' \
     --header 'content-type: application/json' \
     --data '{"query":"{ clients { pageInfo { hasNextPage } edges { node { id, name } } } }"}'
</pre>

Following examples describe uniquely the graphQL query (that has to be serialized into the JSON)

### Clients

#### List clients

<pre class="prettyprint lang-js">
query {
    clients(first: 10, after: "Y3Vyc29yMQ==") {
      edges {
        node {
          id
          name
        }
      }
    }
  }
</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "clients": {
      "edges": [
        {
          "node": {
            "id": 335,
            "name": "R&D Boss"
          }
        }
      ]
    }
  }
}
</pre>

#### Get client by identifier

<pre class="prettyprint lang-js">
query {
    client(clientId: 335) {
      id
      name
    }
  }

</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "client": {
      "id": 335,
      "name": "R&D Boss"
    }
  }
}
</pre>

### Connectors

#### Get connector by identifier

<pre class="prettyprint lang-js">
query {
    connector(id: 41c64064-4729-4d83-a939-8d46ac06d207) { 
        name 
        isPrivate 
        createdAt
    }
}
</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "connector": {
      "name": "My connector",
      "isPrivate": false,
      "createdAt": "2019-07-03T11:25:38Z"
    }
  }
}
</pre>

### Projects

#### List projects

<pre class="prettyprint lang-js">
query {
    projects(first: 10, after: "Y3Vyc29yMQ==") {
      edges {
        node {
          id
          name
        }
      }
    }
  }
</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "projects": {
      "edges": [
        {
          "node": {
            "id": 335,
            "name": "R&D Boss"
          }
        }
      ]
    }
  }
}
</pre>

#### Get project by identifier

<pre class="prettyprint lang-js">
query {
    project(projectId: 335) {
      id
      name
    }
  }

</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "project": {
      "id": 335,
      "name": "R&D Boss"
    }
  }
}
</pre>

### Satisfaction survey responses

#### Get the 100 first responses to the satisfaction survey during the given time interval:

<pre class="prettyprint lang-js">
query {
    satisfactionSurveyResponses(
        projectIds: [1,2], 
        interval: {
	    from: "2019-01-04T00:00:00+01:00",
	    to: "2019-01-04T23:59:59+01:00"
        }
    ) {
    edges {
      node {
        customerSatisfaction,
        netPromoterScore,
        satisfactionComment,
        conversation {
          id,
          createdAt,
          closedAt,
          project {
            id,
            name,
          },
          agents {
            id,
            firstName,
            lastName,
            __typename
          }
        }
      }
    },
    pageInfo {
      endCursor
      hasNextPage
    }
  }
}
</pre>

<pre class="prettyprint lang-js">
{
  "data": {
    "satisfactionSurveyResponses": {
      "edges": [
        {
          "node": {
            "customerSatisfaction": 5,
            "netPromoterScore": 10,
            "satisfactionComment": "Rapide",
            "conversation": {
              "id": "d42d8291-6542-4eed-bb44-988e5264fc2d",
              "createdAt": "2019-01-04T11:12:13Z",
              "closedAt": "2019-01-04T12:13:14Z",
              "project": {
                "id": 1,
                "name": "My brand online"
              },
              "agents": [
                {
                  "id": 30,
                  "firstName": null,
                  "lastName": "Wall-e",
                  "type": "bot"
                },
                {
                  "id": 31,
                  "firstName": "Jean",
                  "lastName": "Robert",
                  "__typename": "Expert"
                }
              ]
            }
          }
        }
      ],
      "pageInfo": {
        "endCursor": "MTU0NjU5NzY5MjAwMCYmMmVhMTYyZjgtNTlkZC00MzkxLTljNTMtMmJkNjM2YzFlNWU1",
        "hasNextPage": true
      }
    }
  }
}
</pre>
