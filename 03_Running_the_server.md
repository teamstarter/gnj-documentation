---
title: Running the server
metaTitle: Running the server
sidebar: Documentation
hideAnchor: false
showTitle: true
---

## Table of contents

1. [Getting started](index.md)
2. [What's a Job/Batch/Pipeline](02_Whats_a_Job_Batch_Pipeline.md)
3. Running the server
4. [Creating a worker](04_Creating_a_worker.md)
5. [The GNJ API](05_The_GNJ_API.md)
6. [Plugin the server to your express](06_Plugin_the_server_to_your_express.md)
7. [Q&A](07_Q%26A.md)
8. [Contributing](08_Contributing.md)

---

## Available commands

---

### Start the default server

GNJ provides a out-of-the-box server if needed:

```
npx gnj run
```

When the server is started, you can open the following url : http://localhost:8080/graphql and discover the schema. If it's the first time you run it, an Sqlite database will be created in the "./data" folder relative to the path you started it.  
You can also run the following command to run a server with a specific database.

```
npx gnj run ./../yourSequelizeConfigFile.js
```

GNJ is build as a micro-service but can also be embedded in your application if needed. We advise to run it and the associated workers with a process manager like [pm2](https://pm2.keymetrics.io/).

---

### Migrate the GNJ schema

```
npx gnj migrate ./../yourSequelizeConfigFile.js //the path from node_modules
```

---

### Start an In-memory server (no DB)

```
npx gnj run-in-memory
```

When the server is started, you can open the following url : http://localhost:8080/graphql and discover the schema. If you shutdown the server, all data will be lost.

---

[Previous: What's a Job/Batch/Pipeline](02_Whats_a_Job_Batch_Pipeline.md)

[Next: Creating a worker](04_Creating_a_worker.md)
