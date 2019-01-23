<template>
  <div class="">
    <div class="columns is-multiline is-3">
      <div v-for="product in allProducts" :key="product.id" class="column is-3">
        <div class="box">
          <img :src="product.images[0].src">
          <p>{{ product.title }}</p>
          <hr>
          <p>starting at: {{ product.variants[0].price }}</p>
          <p>Vender: {{ product.vendor }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import fetch from 'node-fetch'
import Client from 'shopify-buy'

export default {
  data() {
    return {
      allProducts: [],
      errors: []
    }
  },

  // Fetches posts when the component is created.
  created() {
    const client = Client.buildClient(
      {
        domain: 'johnkmeas-dev-test.myshopify.com',
        storefrontAccessToken: '783b792af165d06c17e63781663b77d1'
      },
      fetch
    )
    // Fetch all products in your shop
    client.product.fetchAll().then(products => {
      // Do something with the products
      this.allProducts = products
    })
  }
}
</script>
