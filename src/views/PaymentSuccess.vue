<template>
    <v-app id="inspire">
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md8>
                      <v-container
                      fluid
                      grid-list-md
                      >
                        <v-layout row wrap>
                          <v-flex
                            md12
                            d-flex
                          >
                            <v-card flat tile class="d-flex">
                              <v-img
                                :src="require(`@/assets/images/payments/Payment_successful.png`)"
                                :lazy-src="require(`@/assets/images/payments/Payment_successful.png`)"
                                class="grey lighten-2"
                              >
                                <template v-slot:placeholder>
                                  <v-layout
                                    fill-height
                                    align-center
                                    justify-center
                                    ma-0
                                  >
                                    <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                                  </v-layout>
                                </template>
                              </v-img>
                            </v-card>
                          </v-flex>
                        </v-layout>
                      </v-container>
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
            }
        },
        methods:{
          send_mail(){
            try {
              var self = this
              var oid = localStorage.getItem('order_id')
              var amount = localStorage.getItem('tot_price')
              var mail = localStorage.getItem('user_mail')
              let config = {
                headers: { 'Content-Type': 'application/x-www-form-urlencoded',
                  'x-access-token': localStorage.getItem('token')
                }
              };
              this.$http.post('http://localhost:3000/users/success',{
                order_id:oid,
                total_amount:amount,
                user_mail:mail
              },config)
              .then(function (response) {
                console.log(response);
              })
              .catch(function (error) {
                // handle error
                console.log(error);
              })
            } catch (e) {
              console.log(e);
            }
          }
        },
        mounted(){
          this.send_mail()
        }
    }
</script>
