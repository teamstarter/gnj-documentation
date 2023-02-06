---
title: Getting Started
metaDescription: A job scheduler, a runner and an interface to manage jobs. In one lib.
sidebar: Documentation
hideAnchor: false
rootPage: /contents
date: 2023-01-31
showTitle: true
---


### Prerequisites

To use GNJ, you need a project with:

- Apollo Server V4
- Express
- Sequelize
- [GraphQL-Sequelize-Generator](https://github.com/teamstarter/graphql-sequelize-generator)

A few modules need to be installed, like Graphql-tag, react, WebSocket, etc.

---

### Adding GraphQL-Node-Jobs to your project

```
yarn add graphql-node-jobs
```

To use the api, there is [node-graphql-jobs-react](https://github.com/vincentdesmares/node-jobs-react) that provide convenient Components to list/trigger/delete and other useful actions. It uses Websockets by default to provide a near-realtime experience.
