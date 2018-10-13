<template>
  <div id="login">
    <button class="btn" v-on:click="authenticate">Login with Spotify</button>
  </div>
</template>

<script>
const stateKey = 'spotify_auth_state';

export default {
  methods: {
    generateRandomString: function(length) {
      var text = '';
      var possible = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';

      for (var i = 0; i < length; i++) {
        text += possible.charAt(Math.floor(Math.random() * possible.length));
      }
      return text;
    },
    authenticate: function (event) {
      var client_id = '103b173a2c564c4591fc8af650eff62e'; // Your client id
      var redirect_uri = 'http://50.116.17.227:3000/'; // Your redirect uri

      var state = this.generateRandomString(16);

      sessionStorage.setItem(stateKey, state);
      var scope = 'user-read-private user-read-email';

      var url = 'https://accounts.spotify.com/authorize';
      url += '?response_type=token';
      url += '&client_id=' + encodeURIComponent(client_id);
      url += '&scope=' + encodeURIComponent(scope);
      url += '&redirect_uri=' + encodeURIComponent(redirect_uri);
      url += '&state=' + encodeURIComponent(state);

      console.log(url);

      window.location = url;
    }
  }
}
</script>
