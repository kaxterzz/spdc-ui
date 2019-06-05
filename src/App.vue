<template>
  <v-app id="inspire">
    <v-toolbar>
      <v-toolbar-side-icon>
        <v-icon>card_giftcard</v-icon>
      </v-toolbar-side-icon>
      <v-toolbar-title>Gift Shop</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat to="/">Home</v-btn>
        <template v-if="isLoggedIn == false">
          <v-btn flat to="/login">Login</v-btn>
          <v-btn flat to="/register">Register</v-btn>
        </template>
        <template v-else-if="isLoggedIn == true">
          <v-btn flat to="/products">Products</v-btn>
          <v-btn flat icon @click="logout"><v-icon>power_settings_new</v-icon></v-btn>
        </template>
      </v-toolbar-items>
    </v-toolbar>
    <router-view/>
    <template>
      <v-footer class="pa-3">
        <v-spacer></v-spacer>
        <div>Kasun Ketawala &copy; {{ new Date().getFullYear() }}</div>
      </v-footer>
    </template>
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
    },
    computed : {
      isLoggedIn : function(){ return this.$store.getters.isLoggedIn}
    },
    methods: {
      created: function () {
        this.$http.interceptors.response.use(undefined, function (err) {
          return new Promise(function (resolve, reject) {
            if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
              this.$store.dispatch(logout)
            }
            throw err;
          });
        });
      },
      logout: function () {
        this.$store.dispatch('logout')
        .then(() => {
          this.$router.push('/')
        })
      }
    },
  }
</script>
