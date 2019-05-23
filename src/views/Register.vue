<template>
    <v-app id="inspire">
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md4>
                        <v-card class="elevation-12">
                            <v-toolbar dark color="primary">
                                <v-toolbar-title>Register</v-toolbar-title>
                                <v-spacer></v-spacer>
                            </v-toolbar>
                            <v-card-text>
                                <v-form method="post">
                                    <v-text-field prepend-icon="person" label="Name" type="text" v-model='register.name' required></v-text-field>
                                    <v-text-field prepend-icon="email" label="Email" type="email" v-model='register.email' required></v-text-field>
                                    <v-text-field prepend-icon="phone" label="Phone" type="text" v-model='register.phone' required></v-text-field>
                                    <v-text-field prepend-icon="lock" label="Password" type="password" v-model='register.password' required></v-text-field>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="primary" @click="signup">Register</v-btn>
                            </v-card-actions>
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
                register:{
                  name:'',
                  email:'',
                  phone:'',
                  password:''
                }
            }
        },
        methods:{
          signup: function () {
            let data = {
              name: this.register.name,
              email: this.register.email,
              phone: this.register.phone,
              password: this.register.password,
            }
            this.$store.dispatch('register', data)
           .then(() => this.$router.push('/login'))
           .catch(err => console.log(err))
         }
        },
    }
</script>
