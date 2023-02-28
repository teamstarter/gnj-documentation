---
title: Contributing
metaTitle: Contributing
sidebar: Documentation
hideAnchor: false
showTitle: true
---

## Table of contents

1. [Getting started](index.md)
2. [What's a Job/Batch/Pipeline](02_Whats_a_Job_Batch_Pipeline.md)
3. [Running the server](03_Running_the_server.md)
4. [Creating a worker](04_Creating_a_worker.md)
5. [The GNJ API](05_The_GNJ_API.md)
6. [Plugin the server to your express](06_Plugin_the_server_to_your_express.md)
7. [Q&A](07_Q%26A.md)
8. Contributing

---

### Install the development environment

```console
apt-get install git curl yarn
# or
brew install git curl yarn
```

_node & npm & yarn_

```console
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
nvm install 12
nvm use 12
```

---

### Get the project

```console
git clone git@github.com:teamstarter/node-jobs.git
cd node-jobs
yarn
yarn start
```

---

### Be able to run bin files from the local node_modules folder

```console
vim ~/.bashrc
#Add at the end of the file:
alias npm-exec='PATH=$(npm bin):$PATH'
npm-exec
:wq #Then save and quit
source ~/.bashrc
```

---

### Test the migration script locally

```console
yarn run gnj migrate ./../tests/sqliteTestConfig.js
```

---

### Start a test server using the test database migrated previously

```console
yarn start
```

---

### Running the test

```console
yarn test
```

---

### Debugging a specific test

```console
node --inspect-brk ./node_modules/jest/bin/jest.js ./tests/job.spec.js
```

---

[Previous: Q&A](07_Q%26A.md)
