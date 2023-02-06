---
title: The GNJ API
metaTitle: The GNJ API
sidebar: Documentation
hideAnchor: false
showTitle: true
---

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