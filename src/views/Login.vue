<template>
    <v-app id="inspire">
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md4>
                        <v-card class="elevation-12">
                            <v-toolbar dark color="primary">
                                <v-toolbar-title>Login</v-toolbar-title>
                                <v-spacer></v-spacer>
                            </v-toolbar>
                            <v-form>
                            <v-card-text>

                                    <v-text-field id="email" prepend-icon="person" label="Login" type="email" v-model='login.email' required></v-text-field>
                                    <v-text-field id="password" prepend-icon="lock" label="Password" type="password" v-model='login.password' required></v-text-field>

                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn @click="signin" color="primary">Login</v-btn>
                            </v-card-actions>
                            </v-form>
                        </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
    </v-app>
</template>


<script>
    export default {
        data () {
            return {
                login:{
                  email:'',
                  password:''
                },
            }
        },
        methods:{
          signin: function () {
             let email = this.login.email
             let password = this.login.password
             this.$store.dispatch('login', { email, password })
            .then(() => this.$router.push('/'))
            .catch(err => console.log(err))
          }
        },
    }
</script>
