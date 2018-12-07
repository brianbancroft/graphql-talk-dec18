# Graphql Talk

> _What you want is what you get_

## (Meta) Outline and Timings

- Timeline for how much I'm going to spend talking on the  topics
- 40 Minutes Planned with extension for 50m due to questions
- Talking of each section should not exceed 8m. 2m For questions each


### Introduction

> (what, where, why) 5m

### 1 - Business Overview

> 10m

### 2 - Technical Overview

> 10m

### 3 - Hands-on

> 10m

### Conclusion and Questions

> 5-15m

## Lecture

### Introduction

Hi there, my name is Brian. All of you know me as one of the in-and-out members of the Sparkgeo team. I'm going to spend the next fourty minutes talking about GraphQL.

GraphQL is a specific way of making API requests using rest that is maintainable and iterable in specific use cases, and is used by major content players all over the internet.

I will be starting this lesson with a quick business overview, intended for the non-technical members of Sparkgeo. You're going to know the high-level as this is going to be a noun you will hear more of in the confrence and sales circuts of 2019.

Then I will be breaking off into the technical aspects. Finally in the third part, everyone will get to play with a little hands-on with a sandbox which I've built, for among other reasons, to demo this concept!

- If your eyes water and your souls scream of boredom at the high level stuff, and you _must_ fidget, I have a playground set up already at https://nullislande.rs. Your login, if you want it, is your email address, and the password for this demo is lowercase 'password'. If you want to jump in the graphql, it's nullislande.rs/graphql.

- Likewise if you don't want to get into the weeds, feel free to drop out at the start of part 2.

## Part 1: Business Overview


###  What is GraphQL

GraphQL is a query language in which clients can request things from the server, but only the things which they want. Imagine querying a record that gets you the following attributes:

| Column | Type |
| ------ | ---- |
| id     | string |
| name | string |
| email | string |
| favorite color | string |
| quest | string |
| airspeed_velocity_of_swallow | string |

If you're a mobile developer, and you only want just the name and the email transmitted, you would have to have a modification to the server access point, or a different API endpoint altogether. With a GraphQL endpoint, the client-side developers can choose which attributes to obtain from the request, and which ones not to grab altogether.


In 2012, Facebook built this as a way of allowing mobile and front-end developers to build tighter news feeds, quickly. In 2015, it was publicly released, to which open source communities starting building their own implementations. Then just in November, it became completely open source, and under the reigns of a foundation which answers to the Linux Foundation.

GraphQL is a mature technology, and [npm identified it "a technical force to reckon with in 2019"](https://blog.npmjs.org/post/180868064080/this-year-in-javascript-2018-in-review-and-npms).

![](https://66.media.tumblr.com/d673a9d79f5330f2247e9c8ae62146eb/tumblr_inline_pjbzpiau251ukt7ok_500.png)



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

### Talking to the server
GraphQL query types come in three flavours:

1. `Query` -> I want stuff
2. `Mutarion` -> I want to modify stuff
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
Mutations take up the other sections in a REST CRUD app. Create, Update, Delete.

 > TODO: Explanation
 > TODO: Example of Create
 > TODO: Example of Update
 > TODO: Example of Delete


#### Subscriptions
(not implemented in this application)



### Part 3: Hands-on

Okay. I've talked. Let's walk. In this section, I'm going to demo some queries and mutators. If you want to try yourself, go straight to https://nullislande.rs/graphql.

> All this content is available and abstracted to my best abilities. You can find the example client source code at https://github.com/brianbancroft/nullislanders-spa-client, and the example server source code over at https://github.com/brianbancroft/nullislanders. While the scope of both respositories will change over time, they will both serve and consume GraphQL

#### Creating Queries

- Create a queries for all posts
- Create a query for a single post
- Create a query for all posts with users

#### Creating Mutations
For this exercise, I've left upvoting open without requiring user authentication.

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
