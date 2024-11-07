<template>
  <div class="product-container__list-item">
    <div class="product-container__list-item-image">
      <img :src="'/src/' + product.image.desktop" :alt="product.image.desktop" />
    </div>
    <ButtonCart @onChangeQuantity="(quantity) => getQuantities(quantity)" />
    <div class="product-container__list-item-info">
      <p class="title">{{ product.category }}</p>
      <p class="description">{{ product.name }}</p>
      <p class="price">${{ product.price }}</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { Product } from '@/interfaces/product.model'
import ButtonCart from '../button/ButtonCart.vue'

defineProps<{
  product: Product
}>()

const getQuantities = (quantity: number) => {
  emits('sendQuantity', quantity)
}

const emits = defineEmits<{
  (e: 'sendQuantity', quantity: number): void
}>()
</script>

<style lang="sass" scoped>
.product-container__list-item
    position: relative
    z-index: 0
    width: 32%
    display: flex
    flex-direction: column
    &-image
      width: 100%
      border-radius: 10px
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25)
      img
        border-radius: 10px
        width: 100%
        vertical-align: top
    &-info
      display: flex
      flex-direction: column
      gap: 5px
      .title
        margin: 0
        padding: 0
        font-size: 16px
        font-weight: 400
        color: hsl(7, 20%, 60%)
      .description
        margin: 0
        padding: 0
        font-size: 16px
        font-weight: 600
        color: hsl(14, 65%, 9%)
      .price
        margin: 0
        padding: 0
        font-size: 16px
        font-weight: 700
        color: hsl(14, 86%, 42%)
</style>
