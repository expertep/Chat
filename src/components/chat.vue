<template>
  <div class="columns">
      <div class="column is-2 is-hidden-mobile">
        <aside class="menu">
          <p class="menu-label">
            Friends
          </p>
          <ul class="menu-list">
            <li><a>แหนม</a></li>
          </ul>
        </aside>
      </div>
      <div class="column is-6">
        {{username}}
      </div>
      <div class="column is-4 is-hidden-mobile">
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

</style>
