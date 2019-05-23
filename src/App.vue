<template>
  <v-app id="inspire">
    <v-toolbar>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title>Gift Shop</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat to="/">Home</v-btn>
        <template v-if="authenticated == false">
          <v-btn flat to="/login">Login</v-btn>
          <v-btn flat to="/register">Register</v-btn>
        </template>
        <template v-else-if="authenticated == true">
          <v-btn flat to="/products">Products</v-btn>
        </template>
      </v-toolbar-items>
    </v-toolbar>
    <router-view/>
  </v-app>
</template>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50

#nav
  padding 30px
  a
    font-weight bold
    color #2c3e50
    &.router-link-exact-active
      color #42b983
</style>

<script>
  export default {
    name: 'panel',
    data () {
      return {
        authenticated:false,
      }
    }
  }
</script>
