<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <router-link to="/quotes">Quotes</router-link> |
          <router-link to="/new-quote">New Quote</router-link> |
          <router-link to="/signup">Sign up</router-link> |
          <router-link to="/signin">Sign in</router-link> |
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-xs-12">
          <router-view></router-view>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {}
    }
  }
</script>


<style>
  #app {
    margin: 30px;
  }
</style>
