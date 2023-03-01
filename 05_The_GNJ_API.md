---
title: The GNJ API
metaTitle: The GNJ API
sidebar: Documentation
hideAnchor: false
showTitle: true
---

## Table of contents

1. [Getting started](index.md)
2. [What's a Job/Batch/Pipeline](02_Whats_a_Job_Batch_Pipeline.md)
3. [Running the server](03_Running_the_server.md)
4. [Creating a worker](04_Creating_a_worker.md)
5. The GNJ API
6. [Plugin the server to your express](06_Plugin_the_server_to_your_express.md)
7. [Q&A](07_QA.md)
8. [Contributing](08_Contributing.md)

---

### Everything is exposed as a GraphQL endpoint

You can List, Create, Update and Delete any models.

A few custom mutations are also provided for convenience:

---

#### acquireJob(typeList: [String!]!, workerId: String)

If you use the CRUD query/mutations you will only be able to modify the models without using the full force of GNJ.

**acquireJob** is where the main logic is made. This mutation will mark the first available job as running and assign it to a workerId if given.

You are free to make your own acquire method using the CRUD query/mutations but keep in mind that using API calls might result in transactional problems. If you want to make sure that your custom acquire mutation is perfectly sequential, [use custom mutations](06_Plugin_the_server_to_your_express#you-can-add-custom-mutations-to-the-gnj-server).

#### recoverJob(typeList: [String!]!, workerId: String)

**recoverJob** recover a job by putting it back in the queue with the processing information already acquired.

#### retryJob(typeList: [String!]!, workerId: String)

**retryJob** retry a job which failed.

---

[Previous: Creating a worker](04_Creating_a_worker.md)

[Next : Plugin the server to your express](06_Plugin_the_server_to_your_express.md)

---

### Teamstarter's other libraries

- [GraphQL-Sequelize-Generator](https://teamstarter.github.io/GSG-documentation/)
  - A Graphql API generator based on Sequelize.
- [GraphQL-Web-Hooks](https://teamstarter.github.io/GWH-documentation/)
  - A webhook implementation for GraphQL
