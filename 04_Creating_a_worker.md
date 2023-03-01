---
title: Creating a worker
metaTitle: Creating a worker
sidebar: Documentation
hideAnchor: false
showTitle: true
---

## Table of contents

1. [Getting started](index.md)
2. [What's a Job/Batch/Pipeline](02_Whats_a_Job_Batch_Pipeline.md)
3. [Running the server](03_Running_the_server.md)
4. Creating a worker
5. [The GNJ API](05_The_GNJ_API.md)
6. [Plugin the server to your express](06_Plugin_the_server_to_your_express.md)
7. [Q&A](07_QA.md)
8. [Contributing](08_Contributing.md)

---

You can create your workers from scratch using the Graphql schema. Or you can use the few utilities functions available to quickly setup a worker.

---

## checkForJobs()

```typescript
// Create an ApolloClient that uses your endpoint url
// Here it is using the default url provided by the out-of-the-box server
import {ApolloClient} from "@apollo/client";

const client = New ApolloClient({uri : 'http://localhost:8080/graphql'})
​
const job = await checkForJobs({
  typeList: ['myJobType'],
  client,
  processingFunction: async (job) => {
    const result = await myApiCall()
    return myProcessingFunction(result)
  }
})
```

- **typeList** (Array<String>) is the type of jobs the worker will wait to execute.
- **client** (ApolloClient) is a client with the URL of your GraphQL endpoint.
- **processingFunction** (Function(job, facilities) => Promise<JsonObject>) is the function that executes the job.
- workerId = undefined
- looping = true
- loopTime = 1000

When processingFunction return something, the job is considered as done. The returned Object is serialized and stored as the "output" of the job.

---

### Easy debug without looping

With the looping option to **false** the worker will only check for a job once. Made for end-to-end tests or manual debugging.

```typescript
const job = await checkForJobs({
...,
processingFunction: ...,
looping: false
})
```

---

## Facilities

---

### updateProcessingInfo()

```typescript
const job = await checkForJobs({
  typeList: ["myJobType"],
  client,
  processingFunction: async (job, { updateProcessingInfo }) => {
    await updateProcessingInfo({ percent: 10 });
  },
  looping: false,
});
```

---

## Avoiding spamming your API

Some jobs runs very rarely, so you may want that your worker only check the queue from time to time.

```typescript
const job = await checkForJobs({
...,
processingFunction: ...,
loopTime: 60 \* 1000 // Every minute
})
```

---

## Identifying workers

GNJ automatically generated uuid for your new workers to easily track what went wrong. But if you need to link a run to an id your want you can just specify it under the **workerId** property.

```typescript
const job = await checkForJobs({
...,
processingFunction: ...,
workerId: 'manualCallPreMigration'
})
```

They all use the GraphQL api provided by the server. So even if it's really convenient to use those functions you can create your own.

---

[Previous: Running the server](03_Running_the_server.md)

[Next: The GNJ API](05_The_GNJ_API.md)

---

### Teamstarter's other libraries

- [GraphQL-Sequelize-Generator](https://teamstarter.github.io/gsg-documentation/)
  - A Graphql API generator based on Sequelize.
- [GraphQL-Web-Hooks](https://teamstarter.github.io/gwh-documentation/)
  - A webhook implementation for GraphQL
