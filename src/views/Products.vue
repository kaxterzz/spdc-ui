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
                      <v-layout row wrap>
                        <v-flex md4
                        v-for="product in products"
                        :key="product.name"
                        v-bind="{ [`xs${product.flex}`]: true }"
                        >
                        <v-card
                        class="mx-auto"
                        color="#26c6da"
                        dark
                        max-width="400"
                        >
                        <v-card-title>
                          <span class="title font-weight-light">{{product.name}}</span>
                        </v-card-title>

                        <v-img
                        :src="require(`@/assets/images/products/${product.img_url}`)"
                        >
                      </v-img>

                      <v-card-actions>
                        <v-list-tile-content>
                          <v-btn fab dark small color="primary" @click="add_price(product.price)">
                            <v-icon dark>add_shopping_cart</v-icon>
                          </v-btn>
                        </v-list-tile-content>
                        <v-layout
                        align-center
                        justify-end
                        >
                        <v-icon class="mr-1">info</v-icon>
                        <span class="subheading mr-2">{{product.points}}</span>
                        <span class="mr-1">·</span>
                        <v-icon class="mr-1">attach_money</v-icon>
                        <span class="subheading">{{product.price}}</span>
                      </v-layout>
                    </v-list-tile>
                  </v-card-actions>
                </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
            </v-flex>
            </v-layout>
            </v-container>
        </v-content>
        <v-dialog v-model="more_info" persistent max-width="290">
          <v-card>
            <v-card-title class="headline">Product Price</v-card-title>
            <v-form>
              <v-container>
                <v-layout>
                  <v-flex
                  xs12
                  md12
                  >
                  <v-text-field
                  v-model="qty"
                  label="Quantity"
                  required
                  type="number"
                  min="0"
                  @click="calculate_price"
                  ></v-text-field>
                  <v-text-field
                  v-model="price"
                  label="Price"
                  required
                  type="number"
                  min="0"
                  readonly
                  ></v-text-field>
                </v-flex>
              </v-layout>
            </v-container>
          </v-form>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="green darken-1" flat @click="more_info = false">Cancel</v-btn>
              <v-btn color="green darken-1" flat><v-icon dark>shopping_cart</v-icon></v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
    </v-app>
</template>

<script>
    export default {
        data () {
            return {
                products:[],
                more_info:false,
                qty:0,
                price:0,
                selected_price:0
            }
        },
        methods:{
          load_products(){
            try {
              var self = this
              let config = {
                headers: { 'Content-Type': 'application/x-www-form-urlencoded',
                  'x-access-token': localStorage.getItem('token')
                }
              };
              this.$http.get('http://localhost:3000/products/',config)
              .then(function (response) {
                console.log(response);
                if(response.data.status == 'success'){
                  self.products = response.data.data.products
                }else{
                  self.products = []
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
         add_price(price){
           var self = this
           self.price = 0
           self.qty = 0
           self.selected_price = price
           self.more_info = true
         },
         calculate_price(){
           var self = this
           self.price = self.qty*self.selected_price
         }
        },
        beforeMount() {
          this.load_products()
        }
    }
</script>
