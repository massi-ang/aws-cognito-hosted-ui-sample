<template>
  <div class="home">
     <a class="button button-primary" :href="cognitoLogin">Login with Cognito Hosted UI</a>
  </div>
</template>

<script>
// @ is an alias to /src
const pool = require('@/assets/pool-config.js')
const qs = require('querystring')

export default {
  name: 'Home',
  computed: {
    cognitoLogin: function () {
      var query = {}
      query.redirect_uri = pool.HTTPS_REDIRECT_GW_URI
      query.scope = 'openid'
      query.response_type = 'code'
      query.client_id = pool.CLIENTID
      var uri = pool.HOSTED_UI + '/login?' + qs.stringify(query)
      return uri
    }
  }
}
</script>
