<template>
  <div class="columns main">
      <div class="friendspanel column is-2 is-hidden-mobile">
        <aside class="menu">
          <p class="menu-label">
            Friends
          </p>
          <ul class="menu-list">
            <li v-for="user in users" class="user" :key="user['.key']">
              <span>{{user.username}}</span>
            </li>
          </ul>
        </aside>
      </div>
      <div class="chatpanel column is-6">
        <h1>chat</h1>
        {{username}}

        <div class="field">
          <div class="control">
            <textarea class="textarea" placeholder="Textarea"></textarea>
          </div>
          <div class="control">
            <button class="button is-primary">sent</button>
          </div>
        </div>

      </div>
      <div class="notepanel column is-4 is-hidden-mobile">
        <h1>note</h1>
        <div v-for="doc in note" class="box" :key="doc['.key']">
          {{doc.text}}
        </div>
      </div>
  </div>
</template>

<script>
var firebase = require('firebase')

var config = {
  apiKey: 'AIzaSyD4lqtwAYmjp1B7orDSsztnOxhYAhQfFAk',
  authDomain: 'chat-fda99.firebaseapp.com',
  databaseURL: 'https://chat-fda99.firebaseio.com',
  storageBucket: 'chat-fda99.appspot.com'
}
firebase.initializeApp(config)
var usersRef = firebase.database().ref('users')
var noteRef = firebase.database().ref('note')
export default {
  name: 'chat',
  data () {
    return {
      username: 's'
    }
  },
  firebase: {
    users: usersRef,
    note: noteRef
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .friendspanel {
    background-color: rgb(55,55,55);
    color : white;
  }
  .chatpanel {
    color : white;
    background-color: rgb(46,46,46);
  }
  .notepanel {
    color : white;
    background-color: rgb(46,46,46);
    border-left: 2px solid rgb(69, 69, 69);
  }

</style>
