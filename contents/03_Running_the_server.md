---
title: Running the server
metaTitle: Running the server
sidebar: Documentation
hideAnchor: false
showTitle: true
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
