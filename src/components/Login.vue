<template>
  <div id="login">
    <button class="btn" v-on:click="authenticate">Login with Spotify</button>
  </div>
</template>

<script>
const stateKey = 'spotify_auth_state'

export default {
  methods: {
    generateRandomString: function (length) {
      var text = ''
      var possible = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'

      for (var i = 0; i < length; i++) {
        text += possible.charAt(Math.floor(Math.random() * possible.length))
      }
      return text
    },
    authenticate: function (event) {
      var clientId = '103b173a2c564c4591fc8af650eff62e' // Your client id
      var redirectUri = 'http://50.116.17.227:3000/' // Your redirect uri

      var state = this.generateRandomString(16)

      sessionStorage.setItem(stateKey, state)
      var scope = 'user-library-modify user-modify-playback-state streaming user-read-email user-read-private playlist-modify-private playlist-modify-public'

      var url = 'https://accounts.spotify.com/authorize'
      url += '?response_type=token'
      url += '&client_id=' + encodeURIComponent(clientId)
      url += '&scope=' + encodeURIComponent(scope)
      url += '&redirect_uri=' + encodeURIComponent(redirectUri)
      url += '&state=' + encodeURIComponent(state)

      window.location = url
    }
  }
}
</script>
