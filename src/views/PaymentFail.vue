<template>
    <v-app id="inspire">
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm6 md6>
                      <v-container
                      fluid
                      grid-list-md
                      >
                        <v-layout row wrap>
                          <v-flex
                            md10
                            d-flex
                          >
                            <v-card flat tile class="d-flex">
                              <v-img
                                :src="require(`@/assets/images/payments/Payment_faild.png`)"
                                :lazy-src="require(`@/assets/images/payments/Payment_faild.png`)"
                                aspect-ratio="1"
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
        }
    }
</script>
