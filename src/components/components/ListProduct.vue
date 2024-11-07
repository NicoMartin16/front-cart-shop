<template>
  <div class="product-container">
    <h1>Desserts</h1>
    <div class="product-container__list">
      <CardItem
        v-for="(product, index) in products"
        @sendQuantity="(quantity) => getProductsAdded(quantity, product)"
        :product="product"
        :key="index"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from 'vue'
import CardItem from './card/CardItem.vue'
import type { Product } from '@/interfaces/product.model'

const products = ref<Product[]>([])
const productAdded = ref<Product[]>([])

const getProducts = async (): Promise<Product[]> => {
  const resp = await fetch('/src/assets/data/data.json')
  const data: Product[] = await resp.json()
  return data
}

const getProductsAdded = (quantity: number, product: Product) => {
  product.quantity = quantity
  if (productAdded.value.some((item) => item.name === product.name)) {
    productAdded.value = productAdded.value.map((item) => {
      if (item.name === product.name) {
        item.quantity = quantity
      }
      return item
    })
  } else {
    productAdded.value = [...productAdded.value, product]
  }
  emits('sendProductAdded', productAdded.value)
}

const emits = defineEmits<{
  (e: 'sendProductAdded', productAdded: Product[]): void
}>()

onMounted(async () => {
  products.value = await getProducts()
})
</script>

<style lang="sass" scoped>
.product-container
    padding: 20px
    width: 80%
    display: flex
    flex-direction: column
    gap: 20px
    h1
      font-size: 36px
      font-weight: 700
      color: hsl(14, 65%, 9%)
    &__list
        width: 100%
        display: flex
        flex-direction: row
        flex-wrap: wrap
        gap: 20px
</style>
