---
title: Contributing
metaTitle: Contributing
sidebar: Documentation
hideAnchor: false
showTitle: true
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
