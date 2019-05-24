<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm12 md12>
            <v-container
            fluid
            grid-list-md
            >
            <v-stepper v-model="e1">
              <v-stepper-header>
                <v-stepper-step :complete="e1 > 1" step="1">Your Info</v-stepper-step>

                <v-divider></v-divider>

                <v-stepper-step :complete="e1 > 2" step="2">Cart Info</v-stepper-step>

                <v-divider></v-divider>

                <v-stepper-step step="3">Payment</v-stepper-step>
              </v-stepper-header>

              <v-stepper-items>
                <v-stepper-content step="1">
                  <v-text-field
                    v-model="user_info.name"
                    label="Name"
                    readonly
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.last_name"
                    label="Last Name"
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.email"
                    label="E-mail"
                    readonly
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.phone"
                    label="Phone"
                    readonly
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.address"
                    label="Address"
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.city"
                    label="City"
                  ></v-text-field>
                  <v-text-field
                    v-model="user_info.country"
                    label="Country"
                  ></v-text-field>
                  <v-btn
                  color="primary"
                  @click="e1 = 2"
                  >
                  Continue
                </v-btn>

                <v-btn flat>Cancel</v-btn>
              </v-stepper-content>

              <v-stepper-content step="2">
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
                @click="e1 = 3"
                >
                Continue
              </v-btn>

              <v-btn flat>Cancel</v-btn>
            </v-stepper-content>

            <v-stepper-content step="3">
              <v-form
                 ref="form"
                 method="post"
                 action="https://sandbox.payhere.lk/pay/checkout"
               >
               <input type="hidden" name="merchant_id" value="1212577">    <!-- Replace your Merchant ID -->
              <input type="hidden" name="return_url" value="http://localhost:8080/success">
              <input type="hidden" name="cancel_url" value="http://localhost:8080/products">
              <input type="hidden" name="notify_url" value="http://localhost:8080/fail">
              <v-text-field
                v-model="user_info.name"
                label="Name"
                name="first_name"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="user_info.last_name"
                label="Last Name"
                name="last_name"
              ></v-text-field>
              <v-text-field
                v-model="user_info.email"
                label="E-mail"
                name="email"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="user_info.phone"
                label="Phone"
                name="phone"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="user_info.address"
                label="Address"
                name="address"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="user_info.city"
                label="City"
                name="city"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="user_info.country"
                label="Country"
                name="country"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="product_info.order_id"
                label="Order Id"
                name="order_id"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="product_info.pname"
                label="Product Name"
                name="items"
                readonly
              ></v-text-field>

              <v-text-field
                v-model="product_info.tot_price"
                label="Total Price (LKR)"
                readonly
                name="amount"
              ></v-text-field>
              <input type="hidden" name="currency" value="LKR">
              <v-btn
              color="primary"
              type="submit"
              >
              <v-icon dark>shopping_cart</v-icon>
            </v-btn>
            </v-form>
            <v-btn flat>Cancel</v-btn>
            </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
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
                e1:0,
                user_info:{
                  name:'',
                  last_name:'',
                  email:'',
                  phone:'',
                  address:'',
                  city:'',
                  country:'Sri Lanka'
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
          load_data(){
            var self = this
            var u = JSON.parse(localStorage.getItem('user'))
            var order_id = Math.floor(Math.random()*90000) + 10000;
            self.user_info.name = u.name
            self.user_info.email = u.email
            self.user_info.phone = u.phone
            self.product_info.pname = localStorage.getItem('pname')
            self.product_info.pprice = localStorage.getItem('pprice')
            self.product_info.qty = localStorage.getItem('qty')
            self.product_info.points = localStorage.getItem('points')
            self.product_info.tot_price = localStorage.getItem('tot_price')
            localStorage.setItem('order_id',order_id)
            localStorage.setItem('user_mail',self.user_info.email)
            self.product_info.order_id = order_id
          }
        },
        mounted() {
          this.load_data()
        }
    }
</script>
