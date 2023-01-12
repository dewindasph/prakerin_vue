# vue-token-login

> demo vue + token login demo 

- first time login，Send the account password to the backend
- backend based on```Secret key + username + Expiration```generate Token，return to frontend
- After the front end gets it, it is stored in localStroage and Vuex middle
- Every time a request is sent at header add in Token 
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
