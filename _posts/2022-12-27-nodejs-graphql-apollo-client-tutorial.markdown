---
layout: post
title:  Building Simple NodeJS GraphQL API via Apollo Server example
description:
date:   2022-12-27 00:31:46.882708 -0500
author: sdemian
image:  '/images/graphql-image.jpg'
tags:   [graphql, apollo, nodejs, technology]
tags_color: '#477690'
featured: true
---
GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

> GraphQL is the modern way to create flexible, robust, and strictly-typed APIs.

Today we are going to create a NodeJS GraphQL-API using Apollo Server for our simple **jobs GraphQL API**.

# Prerequisites
- What is [GraphQL](https://graphql.org/)
- Understand what is [GraphQL queries and mutations](https://graphql.org/learn/queries/)
- Understand what is [Schemas and Types](https://graphql.org/learn/schema/)
- You have NodeJS (v8+), I will use NodeJS v19.1.0


# Getting started

## Create new project

Open your terminal and create a new folder for our future project.
Run the following command and <span class="code">cd</span> into the folder.

```bash
mkdir graphql-api-example
cd graphql-api-example
```

Now, use <span class="code">npm</span> (or Yarn) to initialize a new Node.js project.


```javascript
npm init --yes
```

## Install the dependencies

For this tutorial we will need only two dependencies: <span class="code">graphql</span> and <span class="code">pollo-server</span>

```bash
npm install --save graphql apollo-server
```

It should populate the <span class="code">package.json</span> and <span class="code">node_modules</span> folder.

## Create server.js file

All the code for our GraphQL API will go into single file <span class="code">server.js</span>

```bash
touch server.js
```

## Creating schema and query our GraphQL API

### Create a schema

It's useful to have an exact description of the JSON data we can ask from our GraphQL server - what fields can we select? What kinds of objects might they return? What fields are available on those sub-objects? That's where the schema comes in.

GraphQL <span class="code">schema</span> defines <span class="code">structure</span> of our data, which we can query later.
Let's create one.

```javascript
const { gql, ApolloServer} = require('apollo-server');

const typeDefs = gql`
  type Job {
    title: String
    description: String
    featured: Boolean
  }

  type Query {
    jobs: [Job]
  }
`;
```

The <span class="code">Query</span> type is special: it lists all of the available queries that clients can execute, along with the return type for each. In this case, the <span class="code">jobs</span> query returns an array of zero or more <span class="code">Jobs</span>

## Writing resolvers for our query

<span class="code">Resolvers</span> define where the data comes from.

Apollo Server is what we call data-source agnostic — this means that you can fetch data from any source you like (SQL & NoSQL databases, REST APIs, other GraphQL APIs, or even just static JSON).

Let's define <span class="code">jobs</span> data, by adding following code in out <span class="code">server.js</span>

```javascript
const jobs = [
  {
    title: 'Ruby on Rails Software Engineer',
    description: 'Senior Ruby/Rails Engineer',
    featured: true
  },
  {
    title: 'NodeJS Software Engineer',
    description: 'Senior NodeJS Engineer',
    featured: false
  }
];
```

Now we have some <span class="code">data</span>  to be resolved.
Let's create a <span class="code">resolvers</span> object and connect it to our <span class="code">jobs</span> data.


```javascript
const resolvers = {
  Query: {
    jobs: () => jobs;
  }
}
```

## Configure instance of our GraphQL server

We have our <span class="code">schema</span>, <span class="code">data</span> and <span class="code">resolver</span>, so let's do the final bit of coding to instantiate our server.

Let's write the final code at the end of our <span class="code">server.js</span> file.

```javascript
const server = new ApolloServer({ typeDefs, resolvers });

server.listen({ port: 3000 }).then(({ url }) => {
  console.log(`🏆 Server is listening at ${url}`);
});
```

## Running
Let's run our server from the root of our directory with the command

```bash
node server.js
```

Terminal should output nice log message:

```bash
💪 Server is listening at http://localhost:3000/
```

## Query our GraphQL API server with Apollo Explorer

The [Apollo Studio Explorer](https://www.apollographql.com/docs/graphos/explorer/explorer/) is a powerful web IDE for creating, running, and managing GraphQL operations.

To use the explorer, we’ll head to studio.apollographql.com/dev and create an account (using either GitHub or your email)

Or You can open <span class="code">http://localhost:3000/</span> and click on <span class="code">Query your server</span> button:

![ApolloServer]({{site.baseurl}}/images/2022-12-27-nodejs-graphql-apollo-client-tutorial.png)

And that is it, now You can start quering your GraphQL API server.

![Querying]({{site.baseurl}}/images/2022-12-27-nodejs-graphql-apollo-client-tutorial-query.png)

In the <span class="code">Operation</span> tab, paste the following query and click the <span class="code">SimpleQuery</span> button.

```javascript
{
  jobs {
    title
    description
    featured
  }
}
```

Now You should see the response on the right.

And this is it. Congratulations 🏆 on your first GraphQL API!

## What to do next?

You can go to official page for the Apollo GraphQL Tutorials [here](https://odyssey.apollographql.com/?utm_source=blog&website=https%3A%2F%2Fsdemian.com)

<span class="code">Thank You!</span>