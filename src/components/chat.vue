<template>
  <div class="columns main">
      <div class="friendspanel column is-2 is-hidden-mobile">
        <aside class="menu">
          <p class="menu-label">
            Friends
          </p>
          <ul class="menu-list">
            <li><a>แหนม</a></li>
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
            <button class="button is-primary">Submit</button>
          </div>
        </div>

      </div>
      <div class="notepanel column is-4 is-hidden-mobile">
        <h1>note</h1>
        {{username}}
      </div>
  </div>
</template>

<script>
export default {
  name: 'chat',
  data () {
    return {
      username: 's'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .friendspanel {
    background-color: rgb(55,55,55);
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
  .main {
    height : 50em;
  }
</style>
