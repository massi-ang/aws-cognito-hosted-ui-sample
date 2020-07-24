<template>
    <div>
    <div>{{ query }}</div>
    <button @click="getTokens" class="button">Get Tokens</button>
    <div v-if="idToken.length > 0">
    <label>ID Token</label>
    <div class="token" >{{ idToken }} </div>
    <label>Access Token</label>
    <div class="token" >{{ accessToken }} </div>
    <button class="button" @click="callApi()">Call API</button>
    </div>
    </div>
</template>

<script>
const qs = require('querystring');

const pool = require('@/assets/pool-config.js')
const axios = require('axios')

export default {
    props: ['query'],
    data: function () {
        return {
            accessToken: '',
            idToken: '',
            decodedIdToken: undefined,
            decodedAccessToken: undefined
        }
    },
    template: '',
    methods: {
        getTokens: function () {
            let self = this
            axios.post(pool.HOSTED_UI+'/oauth2/token', qs.stringify({
                grant_type: 'authorization_code', 
                client_id: pool.CLIENTID, 
                scope: 'openid', 
                code: this.query.code,
                redirect_uri: pool.HTTPS_REDIRECT_GW_URI
            }), {
                headers: {
                    "Content-Type": 'application/x-www-form-urlencoded'
                } 
            }).then((res) => {
                self.accessToken = res.data.access_token
                self.idToken = res.data.id_token
            }).catch(console.log)
        },
        callApi: function() {
            var api_gateway_url = 'https://xxxxxxxxxxx.execute-api.eu-west-1.amazonaws.com/demo/';
            axios.get(api_gateway_url, {
                    headers: { 'Authorization' : this.idToken }
            }).then((data) => console.log(data)).catch((err) => console.log(err))

        }
       
    } 
}
</script>