# aws-cognito-hosted-ui-demo

This is a sample code to show case how to retrieve tokens from a Cognito Hosted UI and use them to invoke an API Gateway secured by Cognito.

1. Setup Cognito Hosted UI as described in the [documentation](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-integration.html)
2. Fill-in the `./src/assets/pool-config.js` file with the information from the User Pool you just created:

```
const pool = {
    USER_POOLID: '',
    CLIENTID: '',
    HOSTED_UI: 'https://<domain>.<region>.amazoncognito.com',
    REGION: 'us-east-1',
    ...
}
```
3. Setup the project with the instruction shown below (Project setup)
4. You need to serve the project from an https route as Cognito only accepts HTTPS redirect URL with a FQDN (ie it will not accept https://localhost/ or https://127.0.0.1). 
5. Add the https hosting URI followed by `/done` as the  `HTTPS_REDIRECT_GW_URI` in the `pool-config.js` file

```
const pool = {
    ... 
    HTTPS_REDIRECT_GW_URI: ''
}
```



## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


