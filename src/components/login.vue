<template>
  <div class="login">

    <div class="column is-half is-offset-one-quarter">
      <div class="column">
        <label class="label">Name</label>
        <div class="control">
          <input class="input" type="text" placeholder="name" v-model="username">
        </div>
      </div>
      <div class="column">
        <a class="button is-primary" href="/">
          LOGIN
        </a>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      username: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
