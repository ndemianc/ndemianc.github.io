---
layout: post
title:  Building Simple NodeJS GraphQL API via Apollo Server example
description:
date:   2022-12-27 00:31:46.882708 -0500
author: sdemian
image:  '/images/graphql-image.jpg'
tags:   [kotlin, technology]
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
Run the following command and <span style="color:#d64292">**cd**</span> into the folder.

```bash
mkdir graphql-api-example
cd graphql-api-example
```

Now, use <span style="color:#d64292">**npm**</span> (or Yarn) to initialize a new Node.js project.


```nodejs
npm init --yes
```
