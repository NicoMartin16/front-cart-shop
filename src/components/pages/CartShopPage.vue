<template>
  <div class="cart-shop-container">
    <ListProduct @send-product-added="getProductAdded" />
    <SummaryCart :productsOnCart="productsOnCart" />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import ListProduct from '../components/ListProduct.vue'
import SummaryCart from '../components/summarycart/SummaryCart.vue'
import type { Product } from '@/interfaces/product.model'

const productsOnCart = ref<Product[]>([])

const getProductAdded = (productAdded: Product[]) => {
  productsOnCart.value = productAdded
}
</script>

<style lang="sass" scoped>
.cart-shop-container
  width: 1440px
  margin: 0 auto
  display: flex
  flex-direction: row
  justify-content: space-between
</style>
