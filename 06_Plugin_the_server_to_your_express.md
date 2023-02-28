---
title: Plugin the server to your express
metaTitle: Plugin the server to your express
sidebar: Documentation
hideAnchor: false
showTitle: true
---

## getApolloServer

Call the function **getApolloServer** to get an instance of GNJ GraphQL server.
Here is a full example of a GNJ server plugged to an express app, including live subscription.

```javascript
const { expressMiddleware } = require('@apollo/server/express4')
const express = require('express')
const http = require('http')
const cors = require('cors')
const json = require('body-parser')
const { createContext, EXPECTED_OPTIONS_KEY } = require('dataloader-sequelize')
const setupServer = require('./schema')
const models = require('./models') //Assuming "models" is your import of the Sequelize models folder, initialized by Sequelize-Cli
const { PubSub } = require('graphql-subscriptions')
const { getApolloServer } = require('graphql-node-jobs')
const { WebSocketServer } = require('ws')

const createServer = async (options = {}, globalPreCallback = () => null) => {
  const app = express()
  options = {
    spdy: { plain: true },
    ...options,
  }
  const httpServer = http.createServer(options, app)

  // assume that we have already an apollo server running in your project
  const { server } = setupServer(globalPreCallback, httpServer)
  await server.start()
  //server.applyMiddleware({ app, path: '/graphql' })
  app.use(
    '/graphql',
    cors(),
    json(),
    expressMiddleware(server, {
      context: async ({ req, connection }) => {
        const contextDataloader = createContext(models.sequelize)

        // Connection is provided when a webSocket is connected.
        if (connection) {
          // check connection for metadata
          return {
            ...connection.context,
            [EXPECTED_OPTIONS_KEY]: contextDataloader,
          }
        }
      },
    })
  )

  const pubSubInstance = new PubSub()
  //here we instantiate a websocket server for GNJ
  const wsServer = new WebSocketServer({
    // This is the `httpServer` we created in a previous step.
    server: httpServer,
    // Pass a different path here if app.use
    // serves expressMiddleware at a different path
    path: '/jobs/graphq',
  })

  // your sequelizeConfiguration
  const config = require('./config/config.js')

  // init GNJ server and starting it
  const jobsServer = await getApolloServer(config, {
    wsServer,
    pubSubInstance,
    playground: true,
  })

  //start
  await jobsServer.start()

  //serving the GNJ server in a specifique route using the expressMiddleware
  app.use('/jobs/graphql', cors(), json(), expressMiddleware(jobsServer, {}))

  await new Promise(resolve => {
    httpServer.listen(process.env.PORT || 8080, () => {
      resolve()
    })

    console.log(
      `🚀 Server ready at http://localhost:${process.env.PORT || 8080}/graphql`
    )
  })
  return httpServer
}

const closeServer = async server => {
  await Promise.all([new Promise(resolve => server.close(() => resolve()))])
}

createServer()
```

---

### You can add custom mutations to the GNJ server.

```javascript
return getApolloServer(
  dbConfig,
  // Apollo server config: cache, extensions and co.
  {},
  // You can add custom mutations if needed
  {
    customAcquire: {
      type: new GraphQLObjectType({
        name: 'customAcquire',
        fields: {
          id: { type: GraphQLInt },
        },
      }),
      args: {
        typeList: {
          type: new GraphQLList(GraphQLString),
        },
      },
      resolve: async (source, args, context) => {
        // GNJ models can be retreived with the dbConfig if needed
        const models = getModels(dbConfig)
        // get a job from the db
        const job = await models.job.findByPk(1)
        return job
      },
    },
  }
)
```
