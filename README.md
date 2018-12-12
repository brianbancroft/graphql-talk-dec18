# Graphql Talk

> _What you want is what you get_

## (Meta) Outline and Timings

- Timeline for how much I'm going to spend talking on the  topics
- 40 Minutes Planned with extension for 50m due to questions
- Talking of each section should not exceed 8m. 2m For questions each


### > Introduction

> (what, where, why) 5m

### > 1 - Business Overview

> 10m

### > 2 - Technical Overview

> 10m

### > 3 - Hands-on

> 10m

### > Conclusion and Questions

> 5-15m

## Lecture

### Introduction

Hi there, my name is Brian. All of you know me as one of the in-and-out members of the Sparkgeo team. I'm going to spend the next fourty minutes talking about GraphQL.

GraphQL is a specific way of making API requests using rest that is maintainable and iterable in specific use cases, and is used by major content players all over the internet.

I will be starting this lesson with a high-level business overview, intended for the non-technical members of Sparkgeo. This is something worth knowing as this is going to be a noun you will hear more of in the confrence and sales circuts of 2019.

Then I will be breaking off into the technical aspects. Finally in the third part, everyone will get to play with a little hands-on with a sandbox which I've built, for among other reasons, to demo this concept!

- If your eyes water and your souls scream of boredom at the high level stuff, and you _must_ fidget, I have a playground set up already at https://nullislande.rs. Your login, if you want it, is your email address, and the password for this demo is lowercase 'password'. If you want to jump in the graphql, it's nullislande.rs/graphql.

- Likewise if you don't want to get into the weeds, feel free to drop out at the start of part 2.

## Part 1: Business Overview

In this part, I'm going to talk about GrapqhQL from a high level. What is it? What is it not? How did it come to be?

###  What is GraphQL

GraphQL is a query language in which clients can request things from the server, but only the things which they want.

Imagine you had an existing server endpoint that provisions content for the user. Maybe there's some changes. Graphql allows front-end developers to make changes to what comes from the server, without having to change the code on the server.

If you're a mobile developer, and you only want just the name and the email transmitted, you would have to have a modification to the server access point, or a different API endpoint altogether. With a GraphQL endpoint, the client-side developers can choose which attributes to obtain from the request, and which ones not to grab altogether.




In 2012, Facebook built this as a way of allowing mobile and front-end developers to build tighter news feeds, quickly. In 2015, it was publicly released, to which open source communities starting building their own implementations. Then just in November, it became completely open source, and under the reigns of a foundation which answers to the Linux Foundation.

GraphQL is a mature technology, and [npm identified it "a technical force to reckon with in 2019"](https://blog.npmjs.org/post/180868064080/this-year-in-javascript-2018-in-review-and-npms).

![npm-chart](https://66.media.tumblr.com/d673a9d79f5330f2247e9c8ae62146eb/tumblr_inline_pjbzpiau251ukt7ok_500.png)

### Who else uses it

GraphQL is used by a wide variety of shops and organizations, ranging from Facebook (duh), to shoppify, twitter, coursera, github and Club Med 🏝 .

### Where can GraphQL be used

As with many new technologies, there should be a lot of skepticism toward instant adoption, at least until the early adopters have figured out all the trouble spots first. Now that this has had more than three years to mature, this should be something on the radar of developers and architects. It should not be made a replacement to each and every REST endpoint, but instead a supplement.

GraphQL is useful for client-facing API's where bandwidth and minimizing number of round trips is an important consideration.

- If your API contains a single endpoint that returns one thing, stick with REST
- If your API is a tileserver, stick with REST,
- If minimizing number of SQL Queries is important, have a long think...

_But..._

- If your API serves content for a timeline or feed (facebook, twitter, instragram),
- If your API is an aggregation of microservices; or,
- If managing number of roundtrips or content is important

Consider using GraphQL?


#### Languages which support GraphQL

For server-side, there are many tools available:

- Graphene (Python)
- Apollo Server (Node)
- Graphql-Go (Go)

For the client-side, there is also a series of open-source libraries:

- `Relay` (JS)
- `Apollo-Client` (JS/Node)
- `gql` (Python, Go)

## Part 2: Technical Overview

### Talking to the Server

GraphQL query types come in three flavours:

1. `Query` -> I want stuff
2. `Mutation` -> I want to modify stuff
3. `Subscription` -> I want a real-time feed to stuff

Here, we're going to dive a bit deeper into each of each one

#### Queries

Queries are similar to GET requests in vanilla REST CRUD app - The Read. Here is some stuff that we need.

##### How is it writen

```graphql
  {
    viewer {
      name
      avatarURL
    }
  }
```

##### How is the query sent to the server

```sh
POST https://api.github.com/graphql
  {
  "query": "{ me: viewer { name avatarURL} }"
  }
```

##### What comes back

```json
  {
    "data": {
      "viewer": {
        "name": "Arnaud Lauret",
        "avatarURL": "https://avatars0.githubusercontent.com/u/10104551?v=3"
      }
    }
  }
```

This is only a start. You can obtain related records at the same query. You can also specify individual records as opposed to entire records:

```graphql
{
  post(id: 1) {
    numberVotes
    body
    uri
    user {
      username
      email
    }
  }
}
```

Will return

```json
{
  "data": {
    "post": {
      "numberVotes": null,
      "body": "An Awesome Team",
      "uri": "https://sparkgeo.com/",
      "user": {
        "username": "testadmin",
        "email": "nullislanders-admin@mailinator.com"
      }
    }
  }
}
```

#### Mutations
Mutations take up the other sections in a REST CRUD app. Create, Update, Delete. But instead of having those distinctions, graphql allows the designers to explain the purposes at the naming level.

- Mutations almost always require some arguments, in brackets.
- Mutations will also require the user to return data to the front-end.

##### Example: Authentication

Authentication can be done through mutation (and yes, Authzero does [support graphql in its authentication](https://blog.pusher.com/handling-authentication-in-graphql-auth0/))

```graphql
  mutation AuthenticateExample {
    authenticate(username: "brian", password: "thisisapassword") {
      success
      token
      error {
        message
      }
    }
  }
```

This will return the following:

```json
  {
    "data": {
      "authenticate": {
        "success": true,
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MjMsImVtYWlsIjoiYnJpYW5Ac3BhcmtnZW8uY29tIiwidXNlcm5hbWUiOiJicmlhbiIsImlhdCI6MTU0NDU2MDkwMCwiZXhwIjoxNTc2MTE4NTAwfQ.CrdutXBa5OrihpV3Q1KajG72WJs6Nr-pSQt7yaKEokU",
        "error": null
      }
    }
  }
```

Most graphql clients such as apollo-client can take the resulting JWT, and consume it.

##### Example: Creating new Records

This is the same idea, what you have is a new record:

```graphql
  mutation CreatePost {
    createPost(title: "Highline Beta works with Corporations to acheive innovation and zero deaths", uri: "https://highlinebeta.com/") {
      success
    }
  }
```

The result is both visible on the front-page, as well as in the response:

```json
{
  "data": {
    "createPost": {
      "success": true
    }
  }
}
```

In this section, what I've talked about are queries and mutations. Queries are when you want to get things, while Mutations are when you want to add things. This things can be stacked, and they can be nested as well.

#### Questions

### Part 3: Hands-on

Okay. I've talked. Let's walk. In this section, I'm going to demo some queries and mutators. If you want to try yourself, go straight to [trynullislande.rs/graphql](https://try.nullislande.rs/graphql).

> All this content is available and abstracted to my best abilities. You can find the example client source code at https://github.com/brianbancroft/nullislanders-spa-client, and the example server source code over at https://github.com/brianbancroft/nullislanders. While the scope of both respositories will change over time, they will both serve and consume GraphQL

- Demonstrate a query, live where get all posts for a given user
- Demonstrate how to get the comments of all the posts for a given user
- Demonstrate how to carry out a mutation.


### Conclusion and Questions

Wow. In the last 35 minutes, we've covered a lot of ground. What we've talked about includes:

- What is graphql, when was it, and when could we use it
- Parts of graphql, including queries and mutators
- We also concluded with a run-down of how to do queries and mutators

> _Fin_

## References

These are all the referneces which I used to construct this tech talk:

### Overview

- High Level -> https://graphql.org
- Facebook Draft 2018 - https://facebook.github.io/graphql/draft/
- GraphQL Foundation - https://foundation.graphql.org/

### Libraries

- [GraphQL Python](https://github.com/graphql-python)
- [Apollo Server (Node)](https://www.apollographql.com/docs/apollo-server/)
- [Apollo Client (React)](https://www.apollographql.com/docs/react/)
- [Apollo Client (Angular)](https://www.apollographql.com/docs/angular/)

### Skepticsm
- https://blog.logrocket.com/5-reasons-you-shouldnt-be-using-graphql-61c7846e7ed3
- https://honest.engineering/posts/why-use-graphql-good-and-bad-reasons
- https://scotch.io/tutorials/graphql-the-good-and-the-bad
- https://apihandyman.io/and-graphql-for-all-a-few-things-to-think-about-before-blindly-dumping-rest-for-graphql/


### Technical
- https://hackernoon.com/easy-peasy-graphql-authentication-and-authorization-using-schema-directives-f28f1845da20
- https://www.apollographql.com/docs/graphql-tools/schema-directives.html
- https://medium.com/the-graphqlhub/graphql-and-authentication-b73aed34bbeb
