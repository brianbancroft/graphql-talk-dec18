# Graphql Talk

_What you want is what you get_

## Sections

### Introduction

Hi there, my name is Brian. All of you know me as one of the in-and-out members of the Sparkgeo team. I'm going to spend the next fourty minutes talking about GraphQL.

GraphQL is a specific way of making API requests using rest that is maintainable and iterable in specific use cases, and is used by major content players all over the internet.

I will be starting this lesson with a quick business overview, intended for the non-technical members of Sparkgeo. You're going to know the high-level as this is going to be a noun you will hear more of in the confrence and sales circuts of 2019.

Then I will be breaking off into the technical aspects. If your eyes water and your souls scream of boredom at the high level stuff, and you _must_ fidget, I have a playground set up already at https://nullislande.rs. Your login, if you want it, is your email address, and the password for this demo is lowercase 'password'. If you want to jump in the graphql, it's nullislande.rs/graphql. Likewise if you don't want to get into the weeds, feel free to drop out at the start of part 2.


## Part 1: Business Overview


###  What is GraphQL
  - Timeline

#### Who controls the specification
Last month, Facebook moved GraphQL from its aegis to the GraphQL Foundation, hosted by the Linux Foundation.


### Who else uses it

GraphQL is used by a wide variety of shops and organizations, ranging from Facebook (duh), to shoppify, twitter, coursera, github and Club Med 🏝 .

### Where can GraphQL be used?

As with many new technologies, there should be a lot of skepticism toward instant adoption, at least until the early adopters have figured out all the trouble spots first.


####  Use Cases
    - Two examples of yes
    - Two Examples of no

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
- Query Definitions'
  - Query

#### How is it writen

```graphql
  {
    viewer {
      name
      avatarURL
    }
  }
```

#### How is the query sent to the server

```sh
POST https://api.github.com/graphql
  {
  "query": "{ me: viewer { name avatarURL} }"
  }
```

#### What comes back

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



  - Mutator
  - Subsciption
- Demo of query definition in playground
- Demo of site that consumes it

### Conclusion and Questions



## References

- Facebook Draft 2018 - https://facebook.github.io/graphql/draft/

### Skepticsm
- https://blog.logrocket.com/5-reasons-you-shouldnt-be-using-graphql-61c7846e7ed3
- https://honest.engineering/posts/why-use-graphql-good-and-bad-reasons
- https://scotch.io/tutorials/graphql-the-good-and-the-bad
- https://apihandyman.io/and-graphql-for-all-a-few-things-to-think-about-before-blindly-dumping-rest-for-graphql/

