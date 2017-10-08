<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
// var firebase = require('firebase')

// Initialize Firebase
// TODO: Replace with your project's customized code snippet
/* var config = {
  apiKey: 'AIzaSyD4lqtwAYmjp1B7orDSsztnOxhYAhQfFAk',
  authDomain: 'chat-fda99.firebaseapp.com',
  databaseURL: 'https://chat-fda99.firebaseio.com',
  storageBucket: 'chat-fda99.appspot.com'
}
firebase.initializeApp(config) */

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
