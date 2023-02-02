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

You are free to make your own acquire method using the CRUD query/mutations but keep in mind that using API calls might result in transactional problems. If you want to make sure that your custom acquire mutation is perfectly sequential, [use custom mutations](https://vincent-desmares.gitbook.io/graphql-node-jobs/plugin-the-server-to-your-express#you-can-add-custom-mutations-to-the-gnj-server).
