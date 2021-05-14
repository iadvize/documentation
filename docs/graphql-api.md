# GraphQL API

## Overview <span hidden>GraphQL</span>

### About the GraphQL API

The new iAdvize GraphQL API offers flexibility and the ability to define precisely the data you want to fetch.

One of the power of GraphQL API is to allow you retrieve many resources in one HTTP call and you can request only fields you need.

If you wan to learn more about GraphQL, please check [Learn GraphQL](https://graphql.org/learn/).

Also, a lot of GraphQL clients are available in [Official GraphQL documentation](https://graphql.org/code/#graphql-clients).

### Root endpoint

The REST API has numerous endpoints; the GraphQL API has a single endpoint: `https://api.iadvize.com/graphql`

The endpoint remains constant no matter what operation you perform.

If your environment is on the `SD` platform, your endpoint is: `https://api.iadvize.com/graphql?platform=sd`

### Authentication <span hidden>GraphQL</span>

The iAdvize authentication mecanism uses temporary tokens that has a 24 hours lifetime.

Unlike our REST API, you can generate your own tokens with a user email & password.

⚠️ Please note the following policy on **authentication**:

- 10 logins per minute per user
- 100 logins per minute per ip address

Read the following articles to learn more about authentication and how to:

- [Create an access_token](#create-an-access_token)
- [Authenticate your API calls](#authenticate-your-api-calls)
- [Check the validity of an access_token](#check-the-validity-of-an-access_token)

### GraphiQL

You can run queries on real iAdvize data using GraphiQL, an integrated development environment in your browser that includes docs, syntax highlighting, and validation errors.

https://developers.iadvize.com/tools/graphiql

[Learn how to to use GraphiQL with iAdvize](#using-graphiql)

## Reference <span hidden>GraphQL</span>

### Documentation

View reference documentation to learn about the data types available in the iAdvize GraphQL API schema.

[See static documentation of our GraphQL types, queries and mutation.](/bundles/devplatformapp/graphqldoc/index.html)

### Discovering the GraphQL API

Since graphQL is [introspective](https://graphql.org/learn/introspection/), it means you can query a GraphQL schema for details about itself.

Query `__schema` to list all types defined in the schema and get details about each:

<pre class="prettyprint lang-js">
query {
  __schema {
    types {
      name
      kind
      description
      fields {
        name
      }
    }
  }
}
</pre>

Query `__type` to get details about any type:

<pre class="prettyprint lang-js">
query {
  __type(name: "Conversation") {
    name
    kind
    description
    fields {
      name
    }
  }
}
</pre>

### GraphQL Voyager

With GraphQL Voyager, you can visually explore the iAdvize GraphQL API as an interactive graph.

This is a great tool that represent all the iAdvize GraphQL API as an interactive graph.

[Let's start the journey!](/tools/voyager-view)


## Guides <span hidden>GraphQL</span>

### Create an access_token

You have make a `POST` call on the following endpoint: `https://api.iadvize.com/oauth2/token` and send the following parameters:

| **Parameter**  | **Description**                                  | **Type** | **Mandatory** |
| -------------- | ------------------------------------------------ | -------- | ------------- |
| **username**   | User email                                       | String   | Yes           |
| **password**   | User password                                    | String   | Yes           |
| **grant_type** | Oauth2 grant type (only `password` is supported) | String   | Yes           |

⚠️ Please note that parameters must be sent as `application/x-www-form-urlencoded` 

**Example:**

<pre class="prettyprint lang-sh">
curl  --request POST \
      --url https://api.iadvize.com/oauth2/token \
      --data "username={EMAIL}&password={PASSWORD}&grant_type=password"
</pre>

### Authenticate your API calls

To authenticate an API call just pass the access token in an authorization header.

<pre class="prettyprint lang-sh">
curl  --request POST \
      --url https://api.iadvize.com/graphql \
      --header "Content-Type: application/json" \
      --header "Authorization: Bearer {YOUR_ACCESS_TOKEN}" \
      --data "YOUR_QUERY"
</pre>

### Check the validity of an access_token

You can verify token validity with the authenticated route below.

<pre class="prettyprint lang-sh">
curl  --request GET \
      --url https://api.iadvize.com/_authenticated \
      --header "Authorization: Bearer {YOUR_ACCESS_TOKEN}"
</pre>

If your token is valid, you will receive a response that looks like this:

<pre class="prettyprint lang-js">
{
  "authenticated": true
}
</pre>

If your token is expired or invalid, you will receive the following response:

<pre class="prettyprint lang-js">
{
  "error_description": "access token not valid",
  "error": "invalid_token"
}
</pre>

### Forming queries with GraphQL

Because GraphQL operations consist of multiline JSON, we strongly recommend using the GraphiQL tool to make GraphQL calls. But, you can also use cURL or any other HTTP-speaking library.

While with REST we use HTTP verbs to define the operations to perform, in GraphQL we will use the HTTP POST verb, because you will provide a JSON-encoded body whether you are performing a query or a mutation.

**Here is an example to list all the projects :**

<pre class="prettyprint lang-sh">
curl  --request POST \
      --url https://api.iadvize.com/graphql \
      --header "Content-Type: application/json" \
      --header "Authorization: Bearer {YOUR_ACCESS_TOKEN}" \
      --data "\
      { \
        \"query\": \"{projects { edges { node { id name}}}}\" \
      }"
</pre>

⚠️ **Note**: The string value of `"query"` must escape newline characters or the schema will not parse it correctly. For the `POST` body, use outer double quotes and escaped inner double quotes.

### Using GraphiQL

**Execute GraphQL queries**

* [1. Create an access_token](https://paper.dropbox.com/doc/GraphQL-API--BKuErSqW9yNsRHPu~K1aukzRAg-3Q2elEheFtgSgnXbZSZtG#:uid=843733020809470286902015&h2=Create-an-access_token)
* [2. Open the GraphiQL tool](/tools/graphiql)
* 3. In the header section, add a new **Key** `Authorization` (if it does not already exists).
* 4. Then, in the **Value** field, enter `Bearer <token>`, where `<token>` is the token you generated previously.
  ⚠️ Don’t forget to check the box to enable the header
* 5. and here we go!

You can test your access by querying your projects:

<pre class="prettyprint lang-js">
query {
  projects {
    edges {
      node {
        id
        name
      }
    }
  }
}
</pre>

**The sidebar docs**

The collapsible **Docs** pane on the right side of the Explorer page allows you to browse documentation about the type system.

All types in a GraphQL schema include a `description` field compiled into documentation that is automatically updated.

The **Docs** sidebar contains the same content that is automatically generated from the schema under [Reference](#reference-graphql). It is just formatted differently.

**Using the query variables pane**

If you want to learn more about variables in GraphQL you can read this documentation : https://graphql.org/learn/queries/#variables
