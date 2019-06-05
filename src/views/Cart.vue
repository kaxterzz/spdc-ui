<template>
    <v-app id="inspire">
      <v-content>
          <v-container fluid fill-height>
              <v-layout align-center justify-center>
                  <v-flex xs12 sm8 md8>
                      <v-card>
                        <v-toolbar dark color="primary">
                            <v-toolbar-title>Shopping Cart</v-toolbar-title>
                            <v-spacer></v-spacer>
                        </v-toolbar>
                        <v-card-text>
                        <v-text-field
                          v-model="product_info.order_id"
                          label="Order Id"
                          readonly
                        ></v-text-field>

                        <v-text-field
                          v-model="product_info.pname"
                          label="Product Name"
                          readonly
                        ></v-text-field>

                        <v-text-field
                          v-model="product_info.pprice"
                          label="Item Price (LKR)"
                          readonly
                        ></v-text-field>
                        <v-text-field
                          v-model="product_info.points"
                          label="Points"
                          readonly
                        ></v-text-field>
                        <v-text-field
                          v-model="product_info.qty"
                          label="Qty"
                          readonly
                        ></v-text-field>
                        <v-text-field
                          v-model="product_info.tot_price"
                          label="Total Price (LKR)"
                          readonly
                        ></v-text-field>
                        <v-btn
                        color="primary"
                        @click="add_order"
                        >
                        Save & Checkout
                      </v-btn>
                    </v-card-text>
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
              user:{
                uid:''
              },
              product_info:{
                pname:'',
                pprice:'',
                qty:'',
                points:'',
                tot_price:'',
                order_id:''
              }
            }
        },
        methods:{
          load_cart(){
            var self = this
            var order_id = Math.floor(Math.random()*90000) + 10000;
            localStorage.setItem('order_id',order_id)
            self.product_info.order_id = order_id
            var u = JSON.parse(localStorage.getItem('user'))
            self.user.uid = u._id
            self.product_info.pname = localStorage.getItem('pname')
            self.product_info.pprice = localStorage.getItem('pprice')
            self.product_info.qty = localStorage.getItem('qty')
            self.product_info.points = localStorage.getItem('points')
            self.product_info.tot_price = localStorage.getItem('tot_price')
          },
          goto(){
            var self = this
            self.$router.push('/checkout')
          },
          add_order(){
            try {
              var self = this
              var token = localStorage.getItem('token')
              let config = {
                headers: {
                  'x-access-token': token
                }
              };
              this.$http.post('http://localhost:3000/orders/',{
                product_name:self.product_info.pname,
                quantity:self.product_info.qty,
                total_price:self.product_info.tot_price,
                user_id:self.user.uid
              },config)
              .then(function (response) {
                if(response.data.status=='success'){
                  self.$router.push('/checkout')
                }else{
                  toastr.error(response.data.message)
                }

                console.log(response);
              })
              .catch(function (error) {
                // handle error
                console.log(error);
              })
            } catch (e) {
              console.log(e);
            }
         },
        },
        mounted(){
          this.load_cart()
        }
    }
</script>
