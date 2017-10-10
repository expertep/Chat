<template>
  <div class="columns main">
      <div class="friendspanel column is-2 is-hidden-mobile">
        <aside class="menu">
          <p class="menu-label">
            Friends
          </p>

          <ul class="menu-list">
            <li v-for="user in users" @click="choosefriend(user.id)" :key="user['.key']" v-if="user.id != id">
              <a :class="checkchoose(user.id)">
                {{user.username}}
                <span :class="onlinestatus(user.status)">&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </a>
            </li>
          </ul>
        </aside>
      </div>
      <div class="chatpanel column is-6">
        <h3 class="title is-3">{{chosenfriend}}</h3>

        <div class="level" v-for="text in conversation" :key="text['.key']">
          <div class="level-left message">
            <span class="sentence" v-if="text.sender == chosenfriend && text.receiver == id">
              {{text.word}}
            </span>
          </div>
          <div class="level-right message is-primary">
            <span class="sentence" v-if="text.sender == id && text.receiver == chosenfriend">
              {{text.word}}
            </span>
          </div>
        </div>

        <div class="level">
          <div class="level-left message">
            <span class="sentence" v-for="typing in users" :key="typing['.key']" v-if="typing.id == chosenfriend && typing.tmptext.receiver == id">
              {{typing.tmptext.text}}
            </span>
          </div>
          <div class="level-right message is-primary">
            <span class="sentence" v-if="tmptextA != ''"><p>{{typing}}</p></span>
          </div>
        </div>



              <div class="field has-addons">
                <div class="control">
                  <textarea class="textarea is-danger" rows="1" v-model="tmptextA" type="text" placeholder="What will you say ?" @keyup.enter="sent()">
                  </textarea>
                </div>
                <div class="control">
                  <a class="button  is-medium" @click="sent()">
                    <figure class="image is-24x24">
                      <img src="../assets/sent.png" alt="">
                    </figure>
                  </a>
                </div>
              </div>



      </div>
      <div class="notepanel column is-4 is-hidden-mobile">
        <h1>note</h1>
        <div v-for="doc in note" class="box" :key="doc['.key']">
          {{doc.text}}
        </div>
      </div>
      <p>Click the following button to see the result: </p>

      <form>
         <input type="button" value="Click Me" onclick="getValue();" />
      </form>
  </div>

</template>

<script>
var firebase = require('firebase') // DB

var config = {
  apiKey: 'AIzaSyD4lqtwAYmjp1B7orDSsztnOxhYAhQfFAk',
  authDomain: 'chat-fda99.firebaseapp.com',
  databaseURL: 'https://chat-fda99.firebaseio.com',
  storageBucket: 'chat-fda99.appspot.com'
}
firebase.initializeApp(config)
const db = firebase.database()

var usersRef = db.ref('users')
var noteRef = db.ref('note')
var typingARef = db.ref('/').child('users/001/tmptext/text')
var typingARefrec = db.ref('/').child('users/001/tmptext/receiver')
var typingBRef = db.ref('/').child('users/002')
var conversationRef = db.ref('chat').orderByChild('time').limitToLast(100)
var sentRef = db.ref('chat')
export default {
  name: 'chat',
  data () {
    return {
      username: 's',
      id: '001',
      chosenfriend: '002',
      tmptextA: '',
      tmptextB: '',
      inputtext: ''
    }
  },
  firebase: {
    users: usersRef,
    note: noteRef,
    typingA: typingARef,
    typingB: typingBRef,
    typingArec: typingARefrec,
    conversation: conversationRef,
    sentText: sentRef
  },
  computed: {
    typing () {
      typingARef.set(this.tmptextA)
      typingARefrec.set(this.chosenfriend)
      return this.tmptextA
    }
  },
  methods: {
    choosefriend (index) {
      this.chosenfriend = index
    },
    checkchoose (index) {
      var tmp = ''
      if (this.chosenfriend === index) {
        tmp = 'is-active'
      }
      return tmp
    },
    onlinestatus (status) {
      if (status === 'online') {
        return 'status online'
      }
      return 'status offline'
    },
    sent () {
      if (this.tmptextA !== ' ' || this.tmptextA !== '') {
        var d = new Date()
        var timecode = d.getTime()
        sentRef.push({
          receiver: this.chosenfriend,
          sender: this.id,
          word: this.tmptextA,
          time: timecode
        })
        this.tmptextA = ''
      }
    }
  },
  mounted: {
    getValue () {
      var retVal = prompt('Enter your name : ', 'your name here')
      document.write('You have entered : ' + retVal)
    }
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
    background-color: rgb(46,46,46);
    padding: 30px
  }
  .notepanel {
    color : white;
    background-color: rgb(46,46,46);
    border-left: 2px solid rgb(69, 69, 69);
  }
  .main {
    height : 101vh;
  }
  .chatpanel  .field {
    position: fixed;
    bottom: 20px;

  }
  .textarea {
    width: 40vw;
    min-height: 45px;

  }
  .sentence {
    padding : 10px;
    max-width: 30vw;
  }
  .status {
    border-radius: 50%;
    display: inline;
    font-size: 10px;
    float: right;
    margin-top: 5px;
  }
  .online {
    background-color: #8fdf59;
  }
  .offline {
    background-color: #878787;
  }

</style>
